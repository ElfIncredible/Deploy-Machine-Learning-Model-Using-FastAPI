# Deploy Machine Learning Model Using FastAPI
FastAPI application provides an endpoint for predicting diabetes status based on input features, using a pre-trained machine learning model and scaler. This project consists of two main parts: a server-side application built with FastAPI and a client-side script that interacts with this server. 

The goal of the project is to predict whether a person is diabetic based on their health data.

## Table of Contents
- [Project Overview](#project-overview)
- [Deploy using FastAPI](#deploy-using-fastapi)
  - [FastAPI Application - Server-side](#fastapi-application---server-side)
    - [Imports and Setup](#imports-and-setup)
    - [Create FastAPI Instance](#create-fastapi-instance)
    - [Define Input Model](#define-input-model)
    - [Load Saved Models and Scalers](#load-saved-models-and-scalers)
    - [Define Prediction Endpoint](#define-prediction-endpoint)
    - [Return Response](#return-response)
  - [Client Script - Client-side](#client-script---client-side)
    - [Imports](#imports)
    - [API Endpoint URL](#api-endpoint-url)
    - [Input Data](#input-data)
    - [Convert to JSON](#convert-to-json)
    - [Send POST Request](#send-post-request)
    - [Print Response](#print-response)

## Project Overview
The project demonstrates how to set up a machine learning model as a web service using FastAPI, and how to interact with this service using a Python script. Specifically, it allows users to input health data (such as glucose levels, BMI, age, etc.) and get a prediction on whether the person is likely to have diabetes.

- **Server Side:** Hosts the predictive model and exposes it via a web API.
- **Client Side:** Sends data to the API and prints the prediction.
This setup can be used in real-world scenarios where a web service needs to be built around a machine learning model, enabling easy integration of predictive analytics into other applications.

## Deploy using FastAPI
### FastAPI Application - Server-side
- **Purpose:** The FastAPI application serves as the backend service for making diabetes predictions.
- **Input Model:** The DiabetesInput model defines the structure of the health-related data that the server expects.
- **Prediction Logic:**
  - The server loads a pre-trained machine learning model and a scaler (for data normalization) from files.
  - When the server receives a POST request at the /diabetes_prediction endpoint, it:
    - Converts the input data into a list of features.
    - Scales these features using the scaler.
    - Feeds the scaled data into the model to make a prediction.
    - Returns a message indicating whether the person is diabetic or not based on the model's prediction.

Here’s how it works:
- ### Imports and Setup
  - **FastAPI** and **BaseModel** from fastapi and pydantic are imported to create and manage the API and data validation.
  - **pickle** is used to load pre-trained models and scalers.
  - **json** is imported but not used in this code.

- ### Create FastAPI Instance
  - An instance of **FastAPI** is created and assigned to **app**.

- ### Define Input Model
  - **diabetes_input** is a Pydantic model that defines the structure of the input data expected in the request. It includes the following fields:
    - **Pregnancies** (integer)
    - **Glucose** (integer)
    - **BloodPressure** (integer)
    - **SkinThickness** (integer)
    - **Insulin** (integer)
    - **BMI** (float)
    - **DiabetesPedigreeFunction** (float)
    - **Age** (integer)

- ### Load Saved Models and Scalers
  - **diabetes_model** and diabetes_scaler are loaded from disk using pickle. These are assumed to be pre-trained machine learning models and scalers.

- ### Define Prediction Endpoint
  - @app.post('/diabetes_prediction') is a POST endpoint that receives input data in the form of diabetes_input.
  - input_parameters.dict() converts the input data from the Pydantic model into a dictionary.
  - The dictionary values are extracted and organized into a list.
  - This list is scaled using the diabetes_scaler.
  - The scaled data is fed into the diabetes_model to make a prediction.
  - Based on the prediction (0 or 1), the endpoint returns a message indicating whether the person is diabetic or not.

- ### Return Response
  - The response is a simple string message: "The person is diabetic" or "The person is not diabetic", depending on the model's prediction.
 
## Client Script - Client-side
- **Purpose:** This script acts as a client that sends data to the FastAPI server and receives a prediction.
- **Process:**
  - It defines a set of health metrics for a person.
  - Converts this data into JSON format, which is suitable for sending via HTTP.
  - Sends the data to the FastAPI server via a POST request.
  - Receives and prints the prediction result from the server.
 
Here’s how it works:
- ## Imports
  - **json:** Used to convert Python dictionaries to JSON strings.
  - **requests:** A popular Python library for making HTTP requests.
- ## API Endpoint URL
  - **url = 'http://127.0.0.1:8000/diabetes_prediction':** This is the URL where the FastAPI app is running locally. The /diabetes_prediction endpoint is specifically where you send the data.
- ## Input Data
input_data_for_model is a dictionary containing the health-related information required by the model:
  - **Pregnancies:** Number of times the person has been pregnant.
  - **Glucose:** Blood glucose level.
  - **BloodPressure:** Blood pressure measurement.
  - **SkinThickness:** Thickness of the skin fold.
  - **Insulin:** Insulin level.
  - **BMI:** Body Mass Index.
  - **DiabetesPedigreeFunction:** A function that scores the likelihood of diabetes based on family history.
  - **Age:** Age of the person.
- ## Convert to JSON
  - **input_json = json.dumps(input_data_for_model):** The dictionary is converted to a JSON string, which is the format needed for sending data in the HTTP request.
- ## Send POST Request
  - **response = requests.post(url, data=input_json):** A POST request is made to the specified URL with the input data. The data parameter contains the JSON string to be sent to the server.
- ## Print Response
  - **print(response.text):** The response from the server is printed. This response will be the prediction result from the FastAPI endpoint, telling you whether the person is diabetic or not.
