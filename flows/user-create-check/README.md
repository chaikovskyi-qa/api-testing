# Postman Flow — User Creation & Verification

This project shows a simple **Postman Flow** for working with a user API.  
It includes creating a user, saving the returned `id`, and checking the user data with this `id`.  

---

## Flow Overview
1. **POST /users**  
   - Creates a new user with `name` and `email`  
   - Extracts the `id` from the response  
   - Saves the `id` in a variable (`userId`) for later use  

2. **GET /users/{{userId}}**  
   - Uses the previously saved `userId`  
   - Verifies that the user was successfully created  

---

## Files
- `user-api.postman_collection.json` → Postman collection with two main requests  
- `user-api-environment.json` → Environment variables (`token`, `base_url`, `userId`)  
- `flow-screenshot.png` → Visual overview of the Postman Flow  
- `README.md` → This documentation  

---

## How to Run
1. Import the collection and environment into **Postman**  
2. Set your `name`, `email`, and `token` in the environment  
3. Run the Flow or send requests manually  

---

## Flow Preview
![Flow Preview](./flow.png)
