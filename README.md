# EXPENSA

### Description

A full web application for tracking expenses, where users would log their daily expenses/incomes, and get back daily/monthly/yearly expense reports. 


## Demo

#### To test the setup locally, the following needs to be present/installed:
* JDK (used OpenJDK version 11.0.6).
* Docker (used version 19.03.8-ce).
* Docker Compose (used version 1.25.4).

#### After installing the requirements listed above, do the following:
1. Clone the repository, and navigate to the clone directory.
2. Compile the code, assemble the webapps, and start all the services in Docker by executing this task:
   ```bash
   ./gradlew clean composeUp
   ```
3. Register a user:
   ```bash
   curl -X POST http://localhost:8080/v1/users \
     -H 'Content-Type: application/json' \
     -d '{"email": "test@gmail.com", "name": "test", "password": "Test1234"}'
   ```
4. Login with the created user:
   ```bash
   export TOKEN=$(curl -sX POST http://localhost:8080/v1/access-tokens \
     -H 'Content-Type: application/json' \
     -d '{"email": "test@gmail.com", "password": "Test1234"}' | jq -r .token)
   ```
5. Create a transaction using the access token from the previous step:
   ```bash
   curl -X POST http://localhost:8080/v1/transactions \
     -H 'Content-Type: application/json' \
     -H "X-Access-Token: $TOKEN" \
     -d '{"type": "EXPENSE","amount": "1.23","category": "abc","date": "2017/03/20","comment": "xyz"}'
   ```
6. Query the report using the access token from step 4:
   ```bash
   curl http://localhost:8080/v1/reports/2017/03/20 \
     -H "X-Access-Token: $TOKEN"
   ```
   
   
   
   ## Author
   
   ##### Jean Marie Gustave MBONYINSHUTI
