# Backend Feature Requirements

This document outlines the technical and functional requirements for key backend features of the ALX Airbnb project.

---

## 1. User Authentication

### API Endpoints

- `POST /api/register`
  - **Description**: Registers a new user.
  - **Input**: `{ "email": "user@example.com", "password": "strongPass123" }`
  - **Validation**:
    - Email must be valid and unique.
    - Password must be at least 8 characters.
  - **Output**: `{ "message": "User registered successfully", "userId": "abc123" }`
  
- `POST /api/login`
  - **Description**: Logs in a registered user.
  - **Input**: `{ "email": "user@example.com", "password": "strongPass123" }`
  - **Output**: `{ "token": "jwt-token", "userId": "abc123" }`
  - **Validation**:
    - Credentials must match a registered user.

### Performance Criteria
- Response time < 500ms for login and registration.
- Passwords must be hashed and stored securely.

---

## 2. Property Management

### API Endpoints

- `POST /api/properties`
  - **Description**: Allows a host to create a new property listing.
  - **Input**:
    ```json
    {
      "title": "Modern Apartment",
      "description": "2 bedroom near the beach",
      "price": 85,
      "location": "Mombasa, Kenya"
    }
    ```
  - **Output**: `{ "message": "Property created", "propertyId": "xyz123" }`
  - **Validation**:
    - Title, description, and location are required.
    - Price must be a positive number.

- `GET /api/properties`
  - **Description**: Returns a list of available properties.
  - **Output**: Array of property objects.

### Performance Criteria
- Database queries must be optimized for filtering and pagination.
- Listings must include at least 3 photos.

---

## 3. Booking System

### API Endpoints

- `POST /api/bookings`
  - **Description**: Create a booking for a property.
  - **Input**:
    ```json
    {
      "propertyId": "xyz123",
      "userId": "abc123",
      "startDate": "2025-06-01",
      "endDate": "2025-06-05"
    }
    ```
  - **Output**: `{ "message": "Booking confirmed", "bookingId": "b123" }`
  - **Validation**:
    - Dates must be valid and non-overlapping.
    - Start date must be before end date.
    - User must be authenticated.

- `GET /api/bookings/:userId`
  - **Description**: Retrieves bookings made by a user.

### Performance Criteria
- Avoid double-booking through locking or conflict resolution.
- Booking confirmation should complete in under 1 second.

---

## General Notes
- All endpoints require authentication via JWT.
- Use HTTPS for all communications.
- Rate limiting enabled on sensitive endpoints (e.g., login, booking).
