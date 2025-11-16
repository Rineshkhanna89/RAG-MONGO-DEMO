d# Goals: New User Story

- Find the related user stories
- Find the related testcases (relationship: user stories --> testcases)
- Generate new testcases

## Additional Steps for Windows

Download and install Node.js (https://nodejs.org/en/download)

If you encounter npm install errors in VS Code terminal:
1. Run PowerShell as 'admin' and execute:
```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
```
or
```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```
2. Now npm install will work in VS Code

## Steps to Implement

1. Extract the zip
2. Open VS Code and add the folder to your workspace
3. Open the terminal, navigate to rag-mongo-demo-v7, and run: `npm install`
4. Open the .env and configure:
   - 4.1) Create database (db_stories_tests) and collection (test_cases)
   - 4.2) Create another collection (user_stories)
   - 4.3) Create testcase vector index (vector_index_test_cases)
         // Refer src/config/testcases-vector-index.json
         // Wait until it reaches Ready state
   - 4.4) Create testcase bm25 index (bm25_search)
         // Refer src/config/testcases-bm25-index.json
         // Wait until it reaches Ready state
   - 4.5) Create user stories vector index (vector_index_user_story)
         // Refer src/config/user-stories-vector-index.json
         // Wait until it reaches Ready state

5. Update the .env with your credentials:
   - Mongo URI, Mistral API, and Groq API

6. Ingestion Pipeline (6000+ docs):
   - 6.1) Open the terminal and run:
         ```
         node ./src/scripts/embeddings/create-embeddings-batch-mistral.js
         ```
   - 6.2) Check the terminal for errors
   - 6.3) Verify data insertion in MongoDB
   - 6.4) Wait until all ingestion is complete
   - 6.5) Test the web app (optional)
   - 6.6) Push stories to MongoDB:
         ```
         node ./src/scripts/embeddings/create-userstories-embeddings-batch-mistral.js
         ```

7. Start the server:
   - 7.1) Run: `npm run dev`
         Front app starts at http://localhost:3000/
   - 7.2) Verify the vector, bm25, and hybrid search in the web app
   - 7.3) Go to Prompt & Schema >> Test & Preview >> Change user story
         Note: Find 3 new user stories under releases
