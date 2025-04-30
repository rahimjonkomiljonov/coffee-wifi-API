Cafe Finder API
Overview
The Cafe Finder API is a Flask-based web API that allows users to manage a database of cafes. You can add new cafes, search for cafes by location, update coffee prices, delete cafes, and retrieve cafe information. The API uses SQLite as the database to store cafe data and is built with Flask and SQLAlchemy.
This project is perfect for learning how to build a RESTful API with Python and Flask!
Features

Retrieve all cafes or a random cafe.
Search for cafes by location.
Add a new cafe to the database.
Update the coffee price of an existing cafe.
Delete a cafe (requires an API key for security).

Prerequisites
Before you start, make sure you have the following installed:

Python 3.x (preferably Python 3.8 or higher)
pip (Python package manager)
A code editor like Visual Studio Code or PyCharm
Postman (optional, for testing the API)

Setup Instructions
1. Clone or Download the Project
If you're using Git, clone the repository to your local machine:
git clone <repository-url>
cd cafe-finder-api

Alternatively, download the project files and navigate to the project folder.
2. Create a Virtual Environment (Optional but Recommended)
A virtual environment keeps your project’s dependencies separate from other projects.

On Windows:python -m venv venv
venv\Scripts\activate


On macOS/Linux:python3 -m venv venv
. venv/bin/activate



After activation, you’ll see (venv) in your terminal.
3. Install Dependencies
The project requires some Python packages listed in requirements.txt. Install them by running:

On Windows:python -m pip install -r requirements.txt


On macOS/Linux:pip3 install -r requirements.txt



This will install Flask, Flask-SQLAlchemy, and other necessary packages.
4. Run the API
Start the API server by running the main script:
python main.py

The API will run on http://localhost:5000 by default. You’ll see a message in the terminal saying the server is running in debug mode.
API Endpoints
1. Home Page

URL: /
Method: GET
Description: Displays the home page (serves index.html).
Example:GET http://localhost:5000/

This will load the homepage in your browser.

2. Get All Cafes

URL: /all
Method: GET
Description: Returns a list of all cafes in the database.
Example:GET http://localhost:5000/all


Response (example):{
    "cafes": [
        {
            "id": 1,
            "name": "The Coffee House",
            "location": "Downtown",
            "map_url": "https://maps.example.com/coffeehouse",
            "img_url": "https://images.example.com/coffeehouse.jpg",
            "seats": "20-30",
            "has_toilet": true,
            "has_wifi": true,
            "has_sockets": false,
            "can_take_calls": true,
            "coffee_price": "£2.50"
        },
        ...
    ]
}



3. Get a Random Cafe

URL: /random
Method: GET
Description: Returns a random cafe from the database.
Example:GET http://localhost:5000/random


Response (example):{
    "cafe": {
        "id": 2,
        "name": "Cafe Mocha",
        "location": "Uptown",
        "map_url": "https://maps.example.com/cafemocha",
        "img_url": "https://images.example.com/cafemocha.jpg",
        "seats": "10-20",
        "has_toilet": false,
        "has_wifi": true,
        "has_sockets": true,
        "can_take_calls": false,
        "coffee_price": "£3.00"
    }
}



4. Search Cafes by Location

URL: /search?loc=<location>
Method: GET
Description: Searches for cafes at the specified location.
Example:GET http://localhost:5000/search?loc=Downtown


Response (success):{
    "cafes": [
        {
            "id": 1,
            "name": "The Coffee House",
            "location": "Downtown",
            "map_url": "https://maps.example.com/coffeehouse",
            "img_url": "https://images.example.com/coffeehouse.jpg",
            "seats": "20-30",
            "has_toilet": true,
            "has_wifi": true,
            "has_sockets": false,
            "can_take_calls": true,
            "coffee_price": "£2.50"
        }
    ]
}


Response (not found):{
    "error": {
        "Not Found": "Sorry, we don't have a cafe at that location."
    }
}



5. Add a New Cafe

URL: /add
Method: POST
Description: Adds a new cafe to the database.
Body: Use x-www-form-urlencoded format with the following fields:
name (string, required)
map_url (string, required)
img_url (string, required)
loc (string, required)
seats (string, required)
has_toilet (boolean, required, e.g., true or false)
has_wifi (boolean, required)
has_sockets (boolean, required)
can_take_calls (boolean, required)
coffee_price (string, optional)


Example (using Postman):
Select POST method.
URL: http://localhost:5000/add
Go to Body → x-www-form-urlencoded and add:name: The Coffee House
map_url: https://maps.example.com/coffeehouse
img_url: https://images.example.com/coffeehouse.jpg
loc: Downtown
seats: 20-30
has_toilet: true
has_wifi: true
has_sockets: false
can_take_calls: true
coffee_price: £2.50




Response (success):{
    "response": {
        "success": "Successfully added the new cafe."
    }
}



6. Update Coffee Price

URL: /update-price/<cafe_id>?new_price=<price>
Method: PATCH
Description: Updates the coffee price of a cafe with the given ID.
Example:PATCH http://localhost:5000/update-price/1?new_price=£5.67


Response (success):{
    "response": {
        "success": "Successfully updated the price."
    }
}


Response (not found):{
    "error": {
        "Not Found": "Sorry a cafe with that id was not found in the database."
    }
}



7. Delete a Cafe

URL: /report-closed/<cafe_id>?api_key=<api-key>
Method: DELETE
Description: Deletes a cafe with the given ID. Requires a valid API key for security.
API Key: The key is TopSecretAPIKey (hardcoded in the code).
Example:DELETE http://localhost:5000/report-closed/1?api_key=TopSecretAPIKey


Response (success):{
    "response": {
        "success": "Successfully deleted the cafe."
    }
}


Response (wrong API key):{
    "error": {
        "Forbidden": "Sorry, that's not allowed. Make sure you have the correct api_key."
    }
}


Response (not found):{
    "error": {
        "Not Found": "Sorry a cafe with that id was not found in the database."
    }
}



Database

The API uses SQLite to store cafe data in a file called cafes.db.
The database is created automatically when you run the app for the first time.
The Cafe table has the following fields:
id (integer, primary key)
name (string, unique, required)
map_url (string, required)
img_url (string, required)
location (string, required)
seats (string, required)
has_toilet (boolean, required)
has_wifi (boolean, required)
has_sockets (boolean, required)
can_take_calls (boolean, required)
coffee_price (string, optional)



Testing with Postman

Download and install Postman (https://www.postman.com/downloads/).
Start the API server (python main.py).
Open Postman and create a new request for each endpoint:
Set the method (GET, POST, PATCH, DELETE).
Enter the URL (e.g., http://localhost:5000/all).
For POST requests, go to Body → x-www-form-urlencoded to add fields.
Click Send to see the response.



Notes

The API runs in debug mode (debug=True), which is great for development but should be turned off in production.
The API key for deleting cafes is hardcoded as TopSecretAPIKey. In a real application, you’d want to store this securely (e.g., in environment variables).
Error handling is implemented for cases like missing cafes or incorrect API keys.

Troubleshooting

Error: “No module named ”Make sure you’ve activated the virtual environment and installed the dependencies (pip install -r requirements.txt).
Error: “Port 5000 is already in use”Another program is using port 5000. Stop the other program or change the port in main.py by adding a port parameter:app.run(debug=True, port=5001)


Database issuesIf cafes.db gets corrupted, delete it and restart the app to create a new one.

Contributing
Feel free to fork this project, make improvements, and submit a pull request! Some ideas for improvement:

Add more endpoints (e.g., get a cafe by ID).
Add input validation for the /add endpoint.
Use environment variables for sensitive data like the API key.

License
This project is for educational purposes and doesn’t have a specific license. Feel free to use and modify it as you like!
