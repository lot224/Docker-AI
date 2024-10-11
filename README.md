
# n8n, Postgres, Ollama, Qdrant Docker Setup for Mac

### Lets GO!!!

  > docker-compose up 

  This will take a little bit as it needs to download the llama 3 LLM. It may look like its frozen, just be patient.

  It will be done when you see:
  ```
  ollama-import-llama-1  | writing manifest 
  ollama-import-llama-1  | success 
  ollama-import-llama-1 exited with code 0
  ```

  Browse to http://localhost:5678

  Setup the owner account (this is all local so it doesn't need anything special)

  First thing you will see is the My workflow screen.

  Click home, click Credentials

  ### Add a Ollama credential
```
  Base URL: `http://host.docker.internal:11434`
```

  ### Add a Postgress credential
```
  Host: `postgres` // this is the container name
  Database: `n8n`
  User: `root`
  Password: `E9pgVgfc83xu` // From the .env file
  ** Leave everything else as is **
```

  ### Add a QdrantApi credential
```
  Qdrant URL: `http://host.docker.internal:6333`
  ** Leave API Key as is **
```


  ## Import chatbot
  Click the more icon (top right, 3 dots)

  Select `Import from File...`

  Find and select the `n8n-workflow-chatbot.json`, click open.

  ### Resolve Exclamation Marks

  Once its imported, we need to resolve the excalamtion marks, we just need to associate the credentials we created with the nodes, everthing else should already be configured.

  ## Ollama Chat Model & Embeddings Ollama & Ollama Model
  ```
  Use the Ollama account
  ```
  ## Progres Chat Memory
  ```
  Use the Progres account
  ```
  
  ## Qdrant Vector Store
  ```
  Use the QdrantApi account
  ```

  ## Save the workflow and exit.
  ```
  Click Save
  Click Home
  Click Add Workflow
  ```

  ## Import the Shared Folder workflow
  Click the more icon (top right, 3 dots)

  Select `Import from File...`

  Find and select the `n8n-workflow-shared-folder.json`, click open.

  ### Resolve Exclamation Marks

  Once its imported, we need to resolve the excalamtion marks, we just need to associate the credentials we created with the nodes, everthing else should already be configured.

  ## Qdrant Vector Store
  ```
  Use the QdrantApi account
  ```
  ## Embeddings Ollama
  ```
  Use the Ollama account
  ```

  ## Save the workflow and exit.
  ```
  Click Save
  Click Home
  ```

## n8n-OPTIONAL-google-doc-scrape.json
  This is an optional workflow for google drive, I haven't implemented this but left it here for future implementation if we wanted too.

# Okay, were done...

  Now what, well we need to turn it on, so you should see that My workflow 2 is currently inactive, toggle it to active.

  Inside the repo, drop any *.md file into it, and it should get processed.

  You can see if its working by opening up the workflow and clicking on Executions (top middle)

  When you drop a file into the shared folder it should spin up processing the document into the Vector Store.

  for extra confirmation you can visit `http://localhost:6333/dashboard` and click on collections to see if the document was processed.

  To try the chat feature, open the My workflow and click chat (bottom middle)