# Deploy Machine Learning Model Using FastAPI


## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Deploy using FastAPI](#deploy-using-fastapi)
  - [Imports and Setup](#imports-and-setup)
  - [Create FastAPI Instance](#create-fastapi-instance)
  - [Define Input Model](#define-input-model)
  - [Load Saved Models and Scalers](#load-saved-models-and-scalers)
  - [Define Prediction Endpoint](#define-prediction-endpoint)

## Project Overview

## Dataset

## Deploy using FastAPI

### Imports and Setup
- **FastAPI** and **BaseModel** from fastapi and pydantic are imported to create and manage the API and data validation.
- **pickle** is used to load pre-trained models and scalers.
- **json** is imported but not used in this code.

### Create FastAPI Instance
- An instance of **FastAPI** is created and assigned to **app**.

### Define Input Model
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
