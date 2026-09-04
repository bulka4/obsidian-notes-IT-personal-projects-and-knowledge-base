Tags: [[__My_projects]]
#MyProjects 

# Introduction
Use the semantic search service (REST API) in the data governance backend
# To do
- In the semantic search route (Ray Serve app), use interfaces for generating embeddings and for searching through a vector database
# New semantic search code architecture
MCP tool returns:
```
[
	[tableID_1, score],
	[tableID_2, score],
	...
]
```
# ChatGPT prompt
can you change this code to use a REST API for semantic search?

```
async function sortDocs(searchedQuery, docs){
    if (searchedQuery == '') return docs

    // fuzzy matching
    const fuse = new Fuse(docs, {keys: ['tableName'], includeScore: true, threshold: 1, findAllMatches:true, ignoreLocation: true})
    const result = fuse.search(searchedQuery)
    // fuzzy_scores[i] is a similarity score for the table with tableId = i.
    // Scores are numbers between 0 and 1. Higher number indicates better match.
    const fuzzy_scores = {}
    result.forEach(x => {
        fuzzy_scores[x.item.tableId] = 1 - x.score
    })

    // make sure that there is a fuzzy score for every document
    docs.forEach(doc => {
        if (isNaN(fuzzy_scores[doc.tableId])) fuzzy_scores[doc.tableId] = 0
    })

    // semantic search
    const model = new Model()
    await model.load_model()

    searchedQueryEncoded = await model.encode(searchedQuery)

    // semantic_scores[i] is a similarity score for the table with tableId = i
    // Scores are numbers between 0 and 1. Higher number indicates better match.
    const semantic_scores = {}

    docs.forEach((doc) => {
        semantic_scores[doc.tableId] = []
        if (doc.tableDescriptionEncoded.length == 0) semantic_scores[doc.tableId].push(0)
        else {
            doc.tableDescriptionEncoded.forEach(vector => {
                semantic_scores[doc.tableId].push(cos_sim(vector, searchedQueryEncoded))
            })
        }
        doc.columns.forEach(column => {
            if (column.columnDescriptionEncoded.length == 0) semantic_scores[doc.tableId].push(0)
            else {
                column.columnDescriptionEncoded.forEach(vector => {
                    semantic_scores[doc.tableId].push(cos_sim(vector, searchedQueryEncoded))
                })
            }
        })

        let max_score = Math.max(...semantic_scores[doc.tableId])
        if (isNaN(max_score))
            semantic_scores[doc.tableId] = 0
        else
            semantic_scores[doc.tableId] = max_score
    })

    // similarity_scores[i] is a similarity score for the table with tableId = i
    // calculated based on scores from both semantic search and fuzzy matching
    const similarity_scores = {}
    docs.forEach((doc) => {
        similarity_scores[doc.tableId] = semantic_scores[doc.tableId] + fuzzy_scores[doc.tableId]
    })

    const sortedDocs = docs.sort((a, b) => {
        if (similarity_scores[a.tableId] > similarity_scores[b.tableId]) return -1
        else if (similarity_scores[a.tableId] < similarity_scores[b.tableId]) return 1
        else return 0
    })

    return sortedDocs
}
```

here `docs` is a collection of mongo documents with the following schema:

```
const col_doc_schema = new mongoose.Schema({
    columnName: {
        type: String,
        required: true
    },
    foreignKey: {
        type: Boolean,
        default: false
    },
    primaryKey: {
        type: Boolean,
        default: false
    },
    columnDescription: {
        type: String
    },
    // columnDescription encoded (changed into a vector) using transformer model for checking sentence similarity
    columnDescriptionEncoded: {
        type: Array
    }
}, {_id: false})

const table_doc_schema = new mongoose.Schema({
    tableId: {
        type: Number,
        required: true
    },
    tableName: {
        type: String,
        required: true
    },
    sourceScript: String,
    tableDescription: {
        type: String
    },
    // tableDescription encoded (changed into a vector) using transformer model for checking sentence similarity
    tableDescriptionEncoded: {
        type: Array
    },
    columns: [col_doc_schema]
}, 
{collection: 'tablesDocs'})
```

Use this rest api route (from a different app):
```
 @app.get("/search")
    async def ask(self, query: str, top_k: int = 3) -> list[dict]:
        """
        Function for semantic search. It returns a list of dictionaries in the following format:
        [
            {
                'object_id': object_id_1,               # ID of the document (taken from the database where this document comes from)
                'similarity_score': similarity_score_1  # Similarity score for this document and the given query
            },
            ...
        ]
        """
        # embedding for the user's query
        sentence_embedding = self.model.run(query)

        results = self.milvus.search(
            collection_name=self.milvus_collection,
            data=sentence_embedding.tolist(),
            anns_field=self.embedding_field_name,
            limit=top_k,
            output_fields=[self.metadata_field_name],
            search_params={"params": {"nprobe": self.nprobe}},
        )

        # Return ID of the document found in the vector database with a similarity score
        return [
            {
                'object_id': result.entity.get(self.metadata_field_name).get(self.object_id_field_name),
                'similarity_score': result.get('distance')
            }
            for result in results[0]
        ]
```

here `object_id` refers to `tableID` from the MongoDB collection