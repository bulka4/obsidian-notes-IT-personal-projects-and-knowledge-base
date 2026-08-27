Tags: [[__My_projects]]
#MyProjects 

# Introduction
We use Node.js for:
- Running a HTTP server for the Data Governance Backend ([[Data governance app with a RAG system - Data governance backend|link]])
- Running JavaScript scripts: Metadata Extraction pipeline ([[Data governance app with a RAG system - Metadata extraction pipeline|link]]) 
# Node.js dependency packages
In the Helm chart we install Node.js dependency packages defined in the `package.json` file by running the `npm install` command.

It creates then the `node_modules` folder and `package-lock.json` file.
# Troubleshooting
Sometimes we might need to remove the `node_modules` folder and `package-lock.json` file before we try to install new packages.