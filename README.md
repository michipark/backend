Michipark API Documentation

Introduction

Welcome to the Michipark API documentation! This API allows you to manage information about cats and their owners. You can use this API to create and retrieve cat records, as well as generate access tokens for cat owners. The API is implemented using Python and Flask.

Base URL

The base URL for all API endpoints is: http://michipark.es/v1/

Endpoints

Get All Cat IDs
Endpoint: /getcats/
Method: GET
Description: Get a list of all cat IDs stored in the system.
Example:
Request:
bash
Copy code
GET http://michipark.es/v1/getcats/
Response:
json
Copy code
[
  "abc123",
  "xyz456",
  "def789"
]
Get Cat Information
Endpoint: /getcat/
Method: GET
Description: Get detailed information about a cat by providing its ID.
Query Parameter:
ID: Cat ID (required)
Example:
Request:
bash
Copy code
GET http://michipark.es/v1/getcat?ID=abc123
Response:
json
Copy code
{
  "ID": "abc123",
  "owner": "John Doe",
  "last_connected": "2 hours ago",
  "time_to_leave": "3 days",
  "last_time_fed": "1 day ago"
}
Add a New Cat
Endpoint: /addcat
Method: POST
Description: Create a new cat with provided information and generate an access token for the cat owner.
Request Body (JSON):
owner: Cat owner's name (optional, default: "Unknown")
last_connected: Time since the cat was last connected (optional, default: "Never")
time_to_leave: Time remaining for the cat to leave (optional, default: "Unknown")
last_time_fed: Time since the cat was last fed (optional, default: "Never")
Example:
Request:
bash
Copy code
POST http://michipark.es/v1/addcat
Content-Type: application/json

{
  "owner": "Alice",
  "last_connected": "1 hour ago",
  "time_to_leave": "2 days",
  "last_time_fed": "12 hours ago"
}
Response:
json
Copy code
{
  "token": "m1ch1T0k3n"
}
Create an Access Token
Endpoint: /createtoken
Method: POST
Description: Generate a random access token for a cat owner. This token can be used to access the cat's information.
Example:
Request:
bash
Copy code
POST http://michipark.es/v1/createtoken
Response:
json
Copy code
{
  "token": "r4nd0mT0k3n"
}
Error Handling

If a requested cat ID is not found, the API will return a 404 error with the following response:
json
Copy code
{
  "error": "Cat not found"
}
If required data is missing in the request body when adding a cat, the API will return a 400 error with the following response:
json
Copy code
{
  "error": "Incomplete data"
}
Rate Limiting

The Michipark API has rate limiting to prevent abuse. The current rate limits are as follows:

100 requests per minute per IP address for non-authenticated endpoints (/getcats/, /getcat/, /createtoken)
50 requests per minute per IP address for authenticated endpoints (/addcat)
Authentication

The /addcat endpoint requires authentication. To access this endpoint, you need to include the access token in the request header as follows:

makefile
Copy code
Authorization: Bearer YOUR_ACCESS_TOKEN
Replace YOUR_ACCESS_TOKEN with the access token obtained from the /createtoken endpoint.

Conclusion

The Michipark API allows you to manage information about cats and their owners easily. You can retrieve a list of all cat IDs, get detailed information about a specific cat, add new cats with their information, and generate access tokens for cat owners. Please ensure that you follow the rate limits and provide the necessary authentication to access the endpoints accordingly. If you have any questions or feedback, feel free to contact us at support@michipark.es. Happy coding!
