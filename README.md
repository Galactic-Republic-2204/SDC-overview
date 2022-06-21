# Backend System Desigin 

## **Description**

I created the backend of product overveiw section with express and database with postgres.  All read queries used by my API will run in under 50ms.
Applied local stress test with k6 on my service in development (on my laptop) with the number of request per second: 1, 10, 100, 1K and the fail_rates are all unders 0.2%

## **Installation**
**_npm install_**: install necessary dependencies for this project.<br>
**_npm start_**: run the client server.<br>
**_npx test_**: run the mocha/chakram testing files.<br>
**_brew install k6_** : install k6 local stress test.<br>


