# API Testing with Postman + GitHub Actions

This project demonstrates basic API testing using **Postman**, **Newman**, and **GitHub Actions CI**.  
It includes positive and negative test scenarios and simple automation in CI.  

---

## Project Structure
- **collections/** → Postman collections (main API, negative scenarios, user API)  
- **envs/** → Postman environments (dev, negative, user)  
- **flows/** → Postman Flows (visual testing scenarios), e.g. user-create-check  
- **.github/workflows/** → GitHub Actions configuration for running Newman tests  

---

## What is implemented
- Postman Flows – create a user and check by ID  
- API Collection – basic requests (GET, POST)  
- Negative tests – 400, 401, 403, 404, 409 with Postman Mock Server  

---

## CI (GitHub Actions)
- Runs collections automatically with **Newman**  
- Generates HTML reports using **htmlextra**  
- Reports available in the *Actions* tab  

---

## How to run locally
1. Install [Newman](https://github.com/postmanlabs/newman):  
   ```bash
   npm install -g newman newman-reporter-htmlextra  
```bash
npm install -g newman newman-reporter-htmlextra

newman run collections/ecommerce.postman_collection.json -e envs/dev.postman_environment.json
newman run collections/negative-mocks.postman_collection.json -e envs/negative-mocks.postman_environment.json

newman run collections/ecommerce.postman_collection.json \
  -e envs/dev.postman_environment.json \
  -r htmlextra --reporter-htmlextra-export reports/report.html
