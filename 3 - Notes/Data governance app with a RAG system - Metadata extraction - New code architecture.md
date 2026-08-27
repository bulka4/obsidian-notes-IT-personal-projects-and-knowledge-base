Tags: [[__My_projects]]
#MyProjects 

# The `main` script
```python
def main():
    # ---------------------------------------------------------
    # Extract metadata
    # ---------------------------------------------------------
    sql = SQLConnector(
        server="DNAPROD",
        database="Stage",
    )

    extractor = MSSQLExtractor(sql)
	# Prepare the metadata variable which is an object of the Metadata dataclass
	# with attributes:
	#   - tables - variable of the list[Table] type with metadata about tables
	#   - scripts - variable of the list[Script] type with metadata about scripts
	#       which will be used to generate data lineage data
    metadata = extractor.extract()


    # ---------------------------------------------------------
    # Create derived data lineage metadata
    # ---------------------------------------------------------
    lineage_creator = DataLineageCreator()
	# Prepare the data_lineage attribute for the metadata variable. 
	# It is of the list[DataLineageDocument] type and contains data lineage data.
	metadata.data_lineage = (
	    lineage_creator.create_data_lineage(metadata)
	)


    # ---------------------------------------------------------
    # Insert metadata into a database used by the data governance backend
    # ---------------------------------------------------------
    inserter = InsertMetadataMongo(
        mongo_uri="mongodb://127.0.0.1:27017",
        database_name="db_doc",
    )

    try:
        inserter.insert(metadata)
    finally:
        inserter.close()


if __name__ == "__main__":
    main()
```
# Data models
## `Metadata`
```python
@dataclass
class Metadata:
	"""
	Represents all the database metadata:
		- tables
		- scripts (using which we can prepare data lineage data)
		- data lineage (prepared based on scripts data)
		  
	This object is used to insert all this data into the database used by the
	data governance backend.
	"""
    tables: list[Table]
    scripts: list[Script]
    data_lineage: list[DataLineageDocument]
```
## `Table`
```python
@dataclass
class Table:
    """
    Represents a SQL table. It will be an element of the Metadata.tables attribute.
    """

    table_id: int
    table_name: str
    source_script: str | None = None
    table_description: str | None = None
    table_description_encoded: list | None = None
    columns: list[Column] = field(default_factory=list)
```
## `Column`
```python
@dataclass
class Column:
    """
    Represents a column belonging to a SQL table. It will be an element of the 
    Metadata.tables[*].columns attribute.
    """

    column_name: str
    foreign_key: bool = False
    primary_key: bool = False
    column_description: str | None = None
    column_description_encoded: list | None = None
```
## `Script`
```python
@dataclass
class Script:
    """
    Represents a script from SQL Server (e.g. view, procedure, etc.).
    
    It will be an element of the Metadata.scripts attribute and will be used
    to prepare data lineage data using the DataLineageCreator interface.
    """

    script_name: str
    script_type: str
    content: str
    # tables/views used by the script
    input_tables: list[str] = field(default_factory=list)
    # table/view produced by the script
    output_table: str | None = None
```
## `DataLineageDocument`
```python
@dataclass
class DataLineageDocument:
	"""
	Represents a document with a data lineage data that can be inserted into a
	NoSQL database, e.g. MongoDB.
	
	The nodes attribute is a list of nodes which
	represent tables and scripts that procudes those tables.
	"""
	data_lineage_id: int
	data_lineage_name: str
	nodes: list[Node]
```
## `Node`
```python
@dataclass
class Node:
	"""
	Represents a single node in the data lineage data. This node can represent a 
	table or a script that produces a table.
	"""
	value: str
	type: str
	linked_to: list[str]
	script: str | None = None
    x: float | None = None
    y: float | None = None
```
# Interfaces
## `MetadataExtractor`
```python
class MetadataExtractor(ABC):
	"""
	Interface for extracting metadata from a chosen database.
	"""
	
    @abstractmethod
    def extract(self) -> Metadata:
        """
        Extract metadata about tables and scripts. 
        
        Returns a Metadata dataclass object with table and script attributes that 
        can be then used as an input for the DataLineageCreator interface which 
        will additionally prepare the data_lineage attribute for the same Metadata 
        dataclass object.
        
        The final Metadata dataclass object with table, script and data_lineage
        attributes can be then used as an input for the InsertMetadata
        interface.
        """
        pass
```
## `DataLineageCreator`
```python
from abc import ABC, abstractmethod
from models.metadata import Metadata

class DataLineageCreator(ABC):
    """
    Interface for operations that derive additional metadata from
    already extracted metadata.
    """

    @abstractmethod
    def create_data_lineage(
        self,
        metadata: Metadata,
    ) -> list[DataLineageDocument]:
        """
        Create data lineage metadata from the extracted metadata about tables
        and scripts.
        
        Returned variable can be set as the data_lineage attribute of the
        Metadata dataclass object so that this object can be used as an input
        for the MetadataInserter interface.
        """
        pass
```
## `InsertMetadata`
```python
class MetadataInserter(ABC):
    """
    Interface for inserting database metadata and data lineage data into a
    database used by the data governance backend. 
	
    The implementation is responsible for translating the common
    Metadata data model into the storage-specific representation.
    """
    
    @abstractmethod
    def create_schemas(self) -> None:
        """
        Create schemas in the destination database where metadata will be saved
        which define data structure (e.g. tables in the SQL or collections in
        the NoSQL).
        """
        pass
        
        
    @abstractmethod
    def insert(self, metadata: Metadata) -> None:
        """
        Insert into a database used by the data governance backend:
	        - tables metadata represented by the metadata.tables variable
	          extracted using the MetadataExtractor interface
		    - a data lineage data represented by the metadata.data_lineage
		      variable prepared using the DataLineageCreator interface 
		"""
        pass
```
# Interface implementations
## `MSSQLExtractor`
This implementation extracts metadata from the MS SQL Server. It returns an object of the `Metadata` data class with `table` and `script` attributes that can be then used as an input for the `DataLineageCreator` interface. 
## `DataLineageCreatorV1`
```python
class DataLineageCreatorV1(DataLineageCreator):
    """
    Creates data lineage documents from extracted scripts to be saved in a
    NoSQL database (e.g. in a MongoDB collection).
    """

    def create_data_lineage(
        self,
        metadata: Metadata,
    ) -> list[DataLineageDocument]:
        """
        The metadata argument is prepared by the MetadataExtractor interface.
     
	    The returned list[DataLineageDocument] variable is a list of data lineage 
	    documents and can be used as the Metadata.data_lineage attribute.
	    
		Such an object of the Metadata dataclass with the data_lineage attribute
		can be used as an input for the InsertMetadata interface.
        """
        final_tables = find_final_tables(
            metadata.scripts
        )

        documents = []

        for data_lineage_id, final_table in enumerate(
            final_tables,
            start=1,
        ):
            document = create_data_lineage_doc(
                final_table=final_table,
                data_lineage_name=final_table,
                scripts=metadata.scripts,
                data_lineage_id=data_lineage_id,
            )

            documents.append(document)

        return documents
        
    def create_data_lineage_doc(
	    final_table: str,
	    data_lineage_name: str,
	    scripts: list[Script],
	    data_lineage_id: int,
	) -> DataLineageDocument:
	    """
	    Create one data lineage document.
	
	    The function corresponds to the old JavaScript
	    `createDataLineageDocs()` + `createNodes()` logic.
	    """
		data_lineage_doc = DataLineageDocument(
		    data_lineage_id=data_lineage_id,
		    data_lineage_name=data_lineage_name,
		    nodes=[],
		)
	
	    _create_nodes(
	        data_lineage_doc=data_lineage_doc,
	        scripts=scripts,
	        table=final_table,
	        first_iteration=True,
	        visited_tables=set(),
	        visited_scripts=set(),
	    )
	
	    return data_lineage_doc
	
	
	def _create_nodes(
	    data_lineage_doc: DataLineageDocument,
	    scripts: list[Script],
	    table: str,
	    first_iteration: bool,
	    visited_tables: set[str],
	    visited_scripts: set[str]
	) -> None:
	    """
	    Recursively create table/script nodes.
	
	    `visited_tables` and `visited_scripts` prevent infinite recursion
	    when SQL objects contain cyclic dependencies.
	    """
```
## `InsertMetadataMongo`
This class owns all MongoDB-specific concerns:
- connecting to MongoDB
- creating collections
- defining MongoDB validation schemas
- converting Python data classes into MongoDB documents
- inserting metadata

It uses as arguments an object of the `Metadata` data class prepared by the `MetadataExtractor` and `DataLineageCreator` interfaces.

It inserts data into the `tablesDocs` and `dataLineageDocs` MongoDB collections.
# Interface implementations compatibility
We use the `Metadata` data model to make all the interfaces implementations compatible, i.e. to make sure that:
- the metadata prepared by the implementation of the `MetadataExtractor`  interface can be used as an input for the implementation of the `InsertMetadata`  interface
- the data lineage data prepared by the implementation of the `DataLineageCreator`  interface can be used as an input for the implementation of the `InsertMetadata`  interface