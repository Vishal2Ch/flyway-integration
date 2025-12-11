this is the project here are the details of project

Your SQL migrations live inside GitHub

Jenkins pulls the migrations

Jenkins runs Flyway to apply them on QA and PROD environments

Jenkins commits back the updated database schema state (if needed) into qa/ and prod/ folders in your GitHub repo

All of this runs on your Windows VM where Jenkins is installed.


here is the architecture of the analogy which is been used

GitHub Repo
 ├── migrations/
 │     ├── V1__init.sql
 │     ├── V2__add_user.sql
 │     └── ...
 ├── qa/
 │     └── state.txt (or schema dump)
 └── prod/
       └── state.txt (or schema dump)

Jenkins Pipeline (runs on Windows VM)
 1. Checkout repo
 2. Run Flyway migrate on QA DB
 3. Export QA schema → save to /qa folder → git commit → push
 4. Run Flyway migrate on PROD DB
 5. Export PROD schema → save to /prod folder → git commit → push
