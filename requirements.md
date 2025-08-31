# Backend Requirement Specifications

This document outlines the requirement specifications for the backend features of the **Airbnb Clone Project**.

---

## 1. User Authentication

### Overview
Handles user registration, login, and authentication using secure methods (hashed passwords, token-based authentication).

### API Endpoints
- `POST /api/auth/register`
  - **Input:** `{ "name": "string", "email": "string", "password": "string" }`
  - **Output (Success):** `{ "message": "User registered successfully", "userId": "uuid" }`
  - **Output (Error):** `{ "error": "Email already exists" }`

- `POST /api/auth/login`
  - **Input:** `{ "email": "string", "password": "string" }`
  - **Output (Success):** `{ "token": "jwt-token", "userId": "uuid" }`
  - **Output (Error):** `{ "error": "Invalid credentials" }`

### Validation Rules
- Email must be valid format and unique in DB.
- Password must be at least 8 characters, include uppercase, lowercase, number.
- Passwords are **hashed** before saving.

### Performance Criteria
- Registration/login requests should complete in **<500ms**.
- Token validation must handle at least **1000 concurrent requests**.

---

## 2. Property Management

### Overview
Enables users to create, update, view, and delete property listings.

### API Endpoints
- `POST /api/properties`
  - **Input:** `{ "title": "string", "description": "string", "location": "string", "price": "number", "userId": "uuid" }`
  - **Output:** `{ "message": "Property created", "propertyId": "uuid" }`

- `GET /api/properties/:id`
  - **Output:** `{ "id": "uuid", "title": "string", "description": "string", "location": "string", "price": "number", "ownerId": "uuid" }`

- `PUT /api/properties/:id`
  - **Input:** `{ "title": "string?", "description": "string?", "price": "number?" }`
  - **Output:** `{ "message": "Property updated" }`

- `DELETE /api/properties/:id`
  - **Output:** `{ "message": "Property deleted" }`

### Validation Rules
- Title and description cannot be empty.
- Price must be a positive number.
- Only the owner can edit or delete their property.

### Performance Criteria
- Property retrieval must support **pagination**.
- API should return search results in **<1s** for 100,000+ records.

---

## 3. Booking System

### Overview
Allows users to book available properties and manage reservations.

### API Endpoints
- `POST /api/bookings`
  - **Input:** `{ "userId": "uuid", "propertyId": "uuid", "checkIn": "date", "checkOut": "date" }`
  - **Output (Success):** `{ "message": "Booking successful", "bookingId": "uuid" }`
  - **Output (Error):** `{ "error": "Property not available" }`

- `GET /api/bookings/:id`
  - **Output:** `{ "bookingId": "uuid", "propertyId": "uuid", "userId": "uuid", "checkIn": "date", "checkOut": "date", "status": "confirmed|cancelled" }`

- `DELETE /api/bookings/:id`
  - **Output:** `{ "message": "Booking cancelled" }`

### Validation Rules
- Check-in date must be before check-out date.
- Property must be available for the given dates.
- Users cannot double-book the same dates.

### Performance Criteria
- Booking conflict check must execute in **<200ms**.
- System must handle at least **500 concurrent bookings**.

---

## Notes
- All APIs use JSON format.
- Authentication is required for all endpoints except registration/login.
- JWT tokens expire in **24 hours**.
- Database must enforce data consistency with constraints and indexes.
