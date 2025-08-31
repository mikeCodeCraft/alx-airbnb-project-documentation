# Backend Requirement Specifications for Airbnb Clone

This document outlines the technical and functional requirements for three key backend features: User Authentication, Property Management, and Booking System.

---

## 1. User Authentication

### API Endpoints
- `POST /api/v1/auth/register`
  - Registers a new user (guest or host)
- `POST /api/v1/auth/login`
  - Authenticates user and returns JWT
- `GET /api/v1/auth/profile`
  - Retrieves authenticated user's profile
- `PUT /api/v1/auth/profile`
  - Updates user profile

### Input/Output Specifications
- **Register**
  - Input: `{ email, password, role, name, profilePhoto }`
  - Output: `{ userId, email, role, token }`
- **Login**
  - Input: `{ email, password }`
  - Output: `{ token, userId, role }`
- **Profile**
  - Input: JWT in header
  - Output: `{ userId, email, name, role, profilePhoto }`

### Validation Rules
- Email must be valid and unique
- Password must be at least 8 characters
- Role must be either 'guest' or 'host'
- Profile photo must be a valid image file

### Performance Criteria
- Registration and login should complete within 1 second
- Token generation and validation must be secure and efficient

---

## 2. Property Management

### API Endpoints
- `POST /api/v1/properties`
  - Create a new property listing
- `GET /api/v1/properties`
  - Retrieve all property listings (with filters)
- `GET /api/v1/properties/:id`
  - Retrieve a specific property
- `PUT /api/v1/properties/:id`
  - Update property details
- `DELETE /api/v1/properties/:id`
  - Delete a property listing

### Input/Output Specifications
- **Create Property**
  - Input: `{ title, description, location, price, amenities, availability, images }`
  - Output: `{ propertyId, hostId, ...propertyDetails }`
- **Retrieve Properties**
  - Input: Query params for filters (location, price, amenities)
  - Output: List of property objects
- **Update/Delete**
  - Input: Property ID, updated fields
  - Output: Success/failure message

### Validation Rules
- Title and description required
- Price must be a positive number
- Location must be valid
- Images must be valid files
- Only hosts can create/edit/delete properties

### Performance Criteria
- Property creation and retrieval should complete within 2 seconds
- Support pagination for large datasets

---

## 3. Booking System

### API Endpoints
- `POST /api/v1/bookings`
  - Create a new booking
- `GET /api/v1/bookings`
  - Retrieve bookings for a user
- `PUT /api/v1/bookings/:id/cancel`
  - Cancel a booking
- `GET /api/v1/bookings/:id`
  - Retrieve booking details

### Input/Output Specifications
- **Create Booking**
  - Input: `{ propertyId, guestId, startDate, endDate }`
  - Output: `{ bookingId, status, totalPrice }`
- **Retrieve Bookings**
  - Input: JWT in header
  - Output: List of booking objects
- **Cancel Booking**
  - Input: Booking ID
  - Output: Success/failure message

### Validation Rules
- Dates must be valid and not overlap with existing bookings
- Property must be available for selected dates
- Only guests can create bookings
- Cancellation must follow policy rules

### Performance Criteria
- Booking creation and cancellation should complete within 2 seconds
- Prevent double bookings with atomic date validation

---

These specifications ensure the backend is robust, secure, and efficient for core Airbnb Clone functionalities.
