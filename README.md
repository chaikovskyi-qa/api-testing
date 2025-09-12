# API Testing with Postman + GitHub Actions

This project demonstrates API testing using **Postman**, **Newman**, and **GitHub Actions CI**.  
It includes both real API flows and negative testing with Postman Mock Server.

---

## 📌 Project Structure

- **collections/**  
  Postman collections (`ecommerce`, `negative-mocks`, `user-api`).

- **envs/**  
  Postman environments (`dev`, `negative-mocks`, `user-api`).

- **flows/**  
  Postman Flows (visual testing scenarios).  
  Example: [user-create-check](flows/user-create-check/flow.png).

- **.github/workflows/**  
  CI configuration for running collections via Newman in GitHub Actions.

---

## 🚀 What is implemented

- **Postman Flows**  
  A flow that creates a user and then retrieves it by ID.  
  ✅ Initially passed successfully (see screenshot in [flows/user-create-check/flow.png](flows/user-create-check/flow.png)).

- **Ecommerce Collection (reqres.in API)**  
  Tests for a public API.  
  ⚠️ Sometimes fails with `401 Unauthorized` because the external API changes its requirements.  
  This was intentionally kept to demonstrate CI catching unstable API behavior.

- **Negative Mocks Collection (400–409)**  
  A set of negative scenarios using Postman Mock Server:  
  - `400 Bad Request`  
  - `401 Unauthorized`  
  - `403 Forbidden`  
  - `404 Not Found`  
  - `409 Conflict`  
  ✅ These tests always pass in CI, since responses are fully controlled.

---

## ⚙️ CI (GitHub Actions)

- The workflow runs **two jobs**:
  1. `run-newman` → runs Ecommerce collection with an HTML report (`htmlextra`) as an artifact.  
  2. `postman` → runs both **Ecommerce** and **Negative Mocks** collections in parallel.  

- Reports are available in the **Actions** tab.

---

## ✅ How to run locally

Install [Newman](https://github.com/postmanlabs/newman):  
```bash
npm install -g newman newman-reporter-htmlextra

newman run collections/ecommerce.postman_collection.json -e envs/dev.postman_environment.json
newman run collections/negative-mocks.postman_collection.json -e envs/negative-mocks.postman_environment.json

newman run collections/ecommerce.postman_collection.json \
  -e envs/dev.postman_environment.json \
  -r htmlextra --reporter-htmlextra-export reports/report.html
