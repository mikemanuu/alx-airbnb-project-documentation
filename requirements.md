# Backend Features Requirement Specifications

This document outlines the technical and functional requirements for the backend features of the system.

## 1. User Authentication

### *Overview*  
Allows users to register, log in, and manage their accounts securely.

### *API Endpoints*
- *POST /api/auth/register*  
  *Input:*  
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string"
  }

Output (Success):

{
  "message": "Registration successful",
  "user_id": "uuid"
}

Output (Failure):

{
  "error": "Email already in use"
}

POST /api/auth/login
Input:

{
  "email": "string",
  "password": "string"
}

Output (Success):

{
  "message": "Login successful",
  "token": "jwt_token"
}

Output (Failure):

{
  "error": "Invalid credentials"
}


Validation Rules

Email: Must be a valid email format.

Password: Minimum 8 characters, includes at least one uppercase, one lowercase, and one special character.

Username: Alphanumeric, 3-20 characters.


Performance Criteria

Registration and login responses must not exceed 300ms.

2. Property Management

Overview

Allows hosts to add, update, view, and delete property listings.

API Endpoints

POST /api/properties
Input:

{
  "title": "string",
  "description": "string",
  "location": "string",
  "price_per_night": "number",
  "host_id": "uuid"
}

Output (Success):

{
  "message": "Property listed successfully",
  "property_id": "uuid"
}

Output (Failure):

{
  "error": "Invalid data format"
}

PUT /api/properties/:id
Input:

{
  "title": "string",
  "description": "string",
  "location": "string",
  "price_per_night": "number"
}

Output:

{
  "message": "Property updated successfully"
}

DELETE /api/properties/:id
Output:

{
  "message": "Property deleted successfully"
}


Validation Rules

Title: Max 100 characters.

Description: Max 500 characters.

Price: Must be a positive number.


Performance Criteria

CRUD operations should respond within 500ms.


3. Booking System

Overview

Enables guests to search for properties, make bookings, and manage them.

API Endpoints

POST /api/bookings
Input:

{
  "property_id": "uuid",
  "guest_id": "uuid",
  "start_date": "date",
  "end_date": "date"
}

Output (Success):

{
  "message": "Booking created successfully",
  "booking_id": "uuid"
}

Output (Failure):

{
  "error": "Property unavailable for selected dates"
}

GET /api/bookings/:id
Output:

{
  "booking_id": "uuid",
  "property_id": "uuid",
  "guest_id": "uuid",
  "start_date": "date",
  "end_date": "date",
  "status": "confirmed/cancelled"
}

DELETE /api/bookings/:id
Output:

{
  "message": "Booking cancelled successfully"
}


Validation Rules

Dates: Start date must be before end date, and no overlaps with existing bookings.


Performance Criteria

Search results must be returned within 200ms.

Booking confirmation must not exceed 400ms.