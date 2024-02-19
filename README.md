# NOT WILL BE UPDATED ANY MORE!
When I saw that there were other projects that do the same thing, I decided not to move forward with this project. from now on, this project will be archived and will not be updated. if you need the same functionality you can search Git Hub for similar projects.

Holland2Stay House Availability API is a Python-based backend service that provides house availability data for the HomeFinderBot. The API scrapes data from the Holland2Stay website and returns up-to-date information about available houses. User-related data like chat_ids from the bot are stored securely in the Firebase Realtime Database. The API, designed using Flask, is hosted on Koyeb and can be accessed at https://favourite-kelcie-mehrab.koyeb.app/


## Key Features

 - Data Scraping: The API scrapes data from the Holland2Stay website to
   provide the most current house availability information.
   
 - User Data Storage: The API stores user-related data like chat_ids from the bot in Firebase Realtime Database.
   
 - End-to-End Service: This API serves as the backend for the
   HomeFinderBot, providing all the data required to serve its users.

## API Endpoints

The API includes the following public endpoints:


*GET h2s/city_names:*
Returns a list of cities available on the Holland2Stay website.

*GET h2s/check_houses/:*
 Returns available houses for a specific city. Requires city_code and available_to_lottery as mandatory parameters.

*GET h2s/list/all:*
 Returns a list of all available houses across all cities, excluding lottery-based availabilities.


The API also includes private endpoints to manage user data stored in Firebase.


## How to Use

To use the API, make requests to the required endpoints. Please note that to access endpoints that require authentication, you need to provide the necessary credentials.


## Installation

To install and run the API locally, follow these steps:

    git clone https://github.com/MHMALEK/holland2stay-daily-house-api.git
    cd holland2stay-daily-house-api
    pip install -r requirements.txt
    export FLASK_APP=app.py
    flask run
    
## Firebase Integration

The Holland2Stay House Availability API uses Firebase Realtime Database for storing user data like chat_ids from the bot. This functionality is encapsulated in the `init_firebase()` function.

Here's a brief overview of how the function works:

`init_firebase()` function retrieves the base64 encoded Firebase service account key from an environment variable `FIREBASE_SERVICE_ACCOUNT_BASE64`. It then decodes this key into a plain string, which is subsequently converted into a dictionary format. This dictionary, representing the service account key, is used to initialize Firebase in the Python environment.

Here's the function for reference:

    def init_firebase():
        # Get the base64 encoded service account key from the environment variable
        base64_service_account_key = os.environ.get("FIREBASE_SERVICE_ACCOUNT_BASE64")
    
        # Decode the service account key
        service_account_key = base64.b64decode(base64_service_account_key).decode("utf-8")
    
        # Convert the service account key to a dictionary
        service_account_info = json.loads(service_account_key)
    
        service_account_info["private_key"] = service_account_info["private_key"].replace(
            "\\n", "\n"
        )
    
        print(service_account_info)
    
        # Use the service account key to authenticate
        cred = credentials.Certificate(service_account_info)
    
        firebase_admin.initialize_app(
            cred,
            {
                "databaseURL": "YOUR_FIREBASE_DATABASE_URL"
            },
        )

### Note for Local Development:

While running the API locally for development purposes, you won't need to initialize Firebase or provide a Firebase service account key. The `init_firebase()` function and its call can be commented out or removed for local testing.

However, if you want to test the full functionality including Firebase, you'll need to obtain a service account key from your Firebase project. This key should be base64 encoded and provided as an environment variable (`FIREBASE_SERVICE_ACCOUNT_BASE64`). Ensure that the Firebase database URL in the `initialize_app` method matches your Firebase Realtime Database's URL.

Please, remember to never expose your Firebase service account key in any public or unsecured context.

## Contributing

We welcome contributions from the developer community. For details on how to contribute, please read the CONTRIBUTING.md file.


## Acknowledgments

We thank all contributors and users for their support in making this project possible.

## Disclaimer and Data Privacy Assurance

The Holland2Stay House Availability API is a free-to-use service intended to provide users with house availability data from the Holland2Stay website. The API is developed with utmost respect for user privacy and data security.

We assure our users that we do not store, use, or share any sensitive personal data. The API only uses data related to user interactions with the bot (like chat_ids) for functionality purposes and this data is securely stored in Firebase Realtime Database.

We strongly discourage the use of this API for any illegal activities. Users are expected to use the API responsibly and in accordance with both local and international laws. The API should only be used for its intended purpose, and any misuse is strictly prohibited.

As the developer, MHMALEK, I am not responsible for any misuse of the API or any actions taken by users that go against these guidelines. Users are responsible for their own actions while using the API, and any consequences resulting from misuse are solely the responsibility of the user.

Please remember to respect others' privacy and use this service responsibly.
