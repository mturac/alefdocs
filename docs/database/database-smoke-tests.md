# Database Smoke Tests

A database example should prove persistence, not just start.

Recommended smoke flow:

1. create a temporary directory
2. start the Alef app with a temp SQLite path
3. create or mutate data through the app
4. query the API to verify the app sees it
5. inspect the SQLite database if the example is about persistence
6. call `/__shutdown`
7. delete the temp directory

Keep database smoke tests credential-free unless the page is specifically about
a live provider.
