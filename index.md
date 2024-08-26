# CoolCard-API

## API Endpoint Documentation
User Messages Listing API
This API endpoint is used to list messages sent by a specific user or messages sent by employees of a corporate manager.

### URL
````http
GET  https://testusecoolcard.online/account/api/zapier
````
### Parameters

| Parameter | Type    | Required | Description                       |
|-----------|---------|----------|-----------------------------------|
| apikey    | String  | YES      | User's API key.                   |

### Headers
- "Content-Type: application/json; charset=utf-8"      
### Response
__Success (200 OK)__   
A successful response returns all messages from the user or corporate manager in JSON format. Messages are sorted by the date they were sent.

### Response Body
````json
[
    {
        "id": 123,
        "uid": "John Doe",
        "kartid": "abc123",
        "ip": "192.168.1.1",
        "country": "Turkey",
        "city": "Istanbul",
        "browser": "Chrome",
        "device": "Desktop",
        "ad": "Reklam",
        "eposta": "john.doe@example.com",
        "telefon": "+905555555555",
        "mesaj": "Bu bir test mesajıdır.",
        "date": "2023-08-26T10:45:00Z",
        "okundu": 1,
        "company": "ABC Corp"
    },
]
````
### Error Cases  
#### 400 Bad Request: API key is missing.

This error occurs if the apikey parameter is not sent or is null.

````json
{
    "error": "API key is missing."
}
````
#### 500 Internal Server Error:   
This error occurs for server-side issues and when the user cannot be found in the database.  

Example response:

````json
{
    "error": "User not found."
}
````
or

````json
{
    "error": "Message not found."
}
````

### Use Cases
#### Getting User Messages
A user can call the API to retrieve their sent messages as follows:  

````http
GET https://testusecoolcard.online/account/api/zapier/?apikey=USER_API_KEY
````

If the user is a corporate manager, the API response will also include messages from the manager's employees.

### Response Sorting
Messages are sorted by date (date field). The newest messages appear at the top.  

#### Notes
-"id": Message ID.  
-"uid": User's name and surname.  
-"kartid": User's card ID.   
-"ip": Visitor's IP address.  
-"country": Visitor's country information.  
-"city": Visitor's city.  
-"browser": Visitor's browser information.  
-"device": Visitor's device type.  
-"ad": Visitor's name and surname information.  
-"eposta": Visitor's email address.  
-"telefon": Visitor's phone number.  
-"mesaj": Visitor's message information.  
-"date": Visitor's message date information. (ISO 8601)  
-"okundu": Message read/unread status.  
-"company": Visitor's company information.   

-"API key: Used to authenticate the user and retrieve related messages."  
*** If a user is a corporate manager, the response will also include messages from the employees under the manager's authority.

#### Example Response
````http
GET https://testusecoolcard.online/account/api/zapier/apikey=your_api_key
````
#### Example Response
````json
[
    {
        "id": 456,
        "uid": "Jane Doe",
        "kartid": "def456",
        "ip": "192.168.1.2",
        "country": "Turkey",
        "city": "Ankara",
        "browser": "Firefox",
        "device": "Mobile",
        "ad": "Kampanya",
        "eposta": "jane.doe@example.com",
        "telefon": "+905556666666",
        "mesaj": "This is another test message.",
        "date": "2023-08-26T11:30:00Z",
        "okundu": 0,
        "company": "XYZ Ltd."
    }
]
````
This documentation provides all the necessary information for developers who want to use the API. It explains how to call the API, which parameters to use, and what response to expect.
