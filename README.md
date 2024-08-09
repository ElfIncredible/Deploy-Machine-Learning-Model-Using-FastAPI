# Deploy Machine Learning Model Using FastAPI
FastAPI application provides an endpoint for predicting diabetes status based on input features, using a pre-trained machine learning model and scaler.

## Table of Contents
- [Project Overview](#project-overview)
- [Deploy using FastAPI](#deploy-using-fastapi)
  - [FastAPI Application - Server-side](#fastapi-application---server-side)
    - [Imports and Setup](#imports-and-setup)
    - [Create FastAPI Instance](#create-fastapi-instance)
    - [Define Input Model](#define-input-model)
    - [Load Saved Models and Scalers](#load-saved-models-and-scalers)
    - [Define Prediction Endpoint](#define-prediction-endpoint)

## Project Overview
This project consists of two main parts: a server-side application built with FastAPI and a client-side script that interacts with this server. The goal of the project is to predict whether a person is diabetic based on their health data.

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

### Load Saved Models and Scalers
- **diabetes_model** and diabetes_scaler are loaded from disk using pickle. These are assumed to be pre-trained machine learning models and scalers.

### Define Prediction Endpoint
- @app.post('/diabetes_prediction') is a POST endpoint that receives input data in the form of diabetes_input.
- input_parameters.dict() converts the input data from the Pydantic model into a dictionary.
- The dictionary values are extracted and organized into a list.
- This list is scaled using the diabetes_scaler.
- The scaled data is fed into the diabetes_model to make a prediction.
- Based on the prediction (0 or 1), the endpoint returns a message indicating whether the person is diabetic or not.

### Return Response
- The response is a simple string message: "The person is diabetic" or "The person is not diabetic", depending on the model's prediction.
