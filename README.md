# Deploy Machine Learning Model Using FastAPI


## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Deploy using FastAPI](#deploy-using-fastapi)
  - [Imports and Setup](#imports-and-setup)
  - [Create FastAPI Instance](#create-fastapi-instance)
  - [Define Input Model](#define-input-model)

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
