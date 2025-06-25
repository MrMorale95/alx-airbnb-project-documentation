# 🚀 Backend Requirement Specifications – ALX Airbnb Clone API

This document provides detailed functional specifications for all backend features, including REST API endpoints, input/output formats, validation rules, and performance expectations.

---

## 👤 Users API

### 📌 Endpoints
- `GET /users/` – List all users  
- `POST /users/` – Create a new user  
- `GET /users/{user_id}/` – Retrieve a specific user  
- `PUT /users/{user_id}/` – Update a specific user  
- `DELETE /users/{user_id}/` – Delete a specific user  

### 📥 Sample Input (POST /users/)
```json
{
  "first_name": "Alice",
  "last_name": "Johnson",
  "email": "alice@example.com",
  "password": "SecurePass123!",
  "phone_number": "+123456789",
  "role": "guest"
}
```

### 📤 Sample Output (GET /users/{user_id}/)
```json
{
  "user_id": "uuid",
  "first_name": "Alice",
  "last_name": "Johnson",
  "email": "alice@example.com",
  "role": "guest",
  "created_at": "2025-06-25T10:00:00Z"
}
```

### ✅ Validation Rules
- `email`: must be unique and valid.
- `password`: minimum 8 characters, includes letters and numbers.
- `role`: must be one of `guest`, `host`, `admin`.

---

## 🏠 Properties API

### 📌 Endpoints
- `GET /properties/` – List all properties  
- `POST /properties/` – Create a new property  
- `GET /properties/{property_id}/` – Retrieve a specific property  
- `PUT /properties/{property_id}/` – Update a specific property  
- `DELETE /properties/{property_id}/` – Delete a specific property  

### 📥 Sample Input (POST /properties/)
```json
{
  "host_id": "uuid",
  "name": "Modern Studio Apartment",
  "description": "Bright and cozy studio downtown.",
  "location": "Lusaka, Zambia",
  "pricepernight": 70.00
}
```

### 📤 Sample Output (GET /properties/{property_id}/)
```json
{
  "property_id": "uuid",
  "host_id": "uuid",
  "name": "Modern Studio Apartment",
  "description": "Bright and cozy studio downtown.",
  "location": "Lusaka, Zambia",
  "pricepernight": 70.00,
  "created_at": "2025-06-25T12:00:00Z",
  "updated_at": "2025-06-25T12:00:00Z"
}
```

### ✅ Validation Rules
- `pricepernight`: must be a positive decimal.
- `name`: 2-100 characters.
- `description`: required.

---

## 📅 Bookings API

### 📌 Endpoints
- `GET /bookings/` – List all bookings  
- `POST /bookings/` – Create a new booking  
- `GET /bookings/{booking_id}/` – Retrieve a specific booking  
- `PUT /bookings/{booking_id}/` – Update a specific booking  
- `DELETE /bookings/{booking_id}/` – Delete a specific booking  

### 📥 Sample Input (POST /bookings/)
```json
{
  "user_id": "uuid",
  "property_id": "uuid",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05",
  "total_price": 280.00
}
```

### 📤 Sample Output (GET /bookings/{booking_id}/)
```json
{
  "booking_id": "uuid",
  "user_id": "uuid",
  "property_id": "uuid",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05",
  "total_price": 280.00,
  "status": "confirmed",
  "created_at": "2025-06-25T14:00:00Z"
}
```

### ✅ Validation Rules
- `start_date` < `end_date`
- Ensure property is available for the selected range.
- `total_price`: must be equal to duration × pricepernight.

---

## 💳 Payments API

### 📌 Endpoint
- `POST /payments/` – Process a payment  

### 📥 Sample Input
```json
{
  "booking_id": "uuid",
  "amount": 280.00,
  "payment_method": "credit_card"
}
```

### 📤 Sample Output
```json
{
  "payment_id": "uuid",
  "booking_id": "uuid",
  "amount": 280.00,
  "payment_method": "credit_card",
  "payment_date": "2025-06-25T15:00:00Z"
}
```

### ✅ Validation Rules
- `amount`: must match `total_price` of the booking.
- `payment_method`: one of `credit_card`, `paypal`, `stripe`.

---

## ⭐ Reviews API

### 📌 Endpoints
- `GET /reviews/` – List all reviews  
- `POST /reviews/` – Create a new review  
- `GET /reviews/{review_id}/` – Retrieve a specific review  
- `PUT /reviews/{review_id}/` – Update a specific review  
- `DELETE /reviews/{review_id}/` – Delete a specific review  

### 📥 Sample Input (POST /reviews/)
```json
{
  "user_id": "uuid",
  "property_id": "uuid",
  "rating": 5,
  "comment": "Fantastic place and great host!"
}
```

### 📤 Sample Output (GET /reviews/{review_id}/)
```json
{
  "review_id": "uuid",
  "user_id": "uuid",
  "property_id": "uuid",
  "rating": 5,
  "comment": "Fantastic place and great host!",
  "created_at": "2025-06-25T16:00:00Z"
}
```

### ✅ Validation Rules
- `rating`: must be between 1 and 5.
- One review per user per property.
- User must have completed a booking for the property.

---

## 🚀 Performance Requirements

| Feature        | Expected Response Time |
|----------------|------------------------|
| User APIs      | < 300ms                |
| Property APIs  | < 300ms                |
| Booking APIs   | < 400ms                |
| Payments       | < 500ms (external API) |
| Reviews        | < 250ms                |

---

## 🔐 Security & Compliance

- JWT Authentication on all routes except `POST /users/` and `/auth/login`.
- Passwords stored using strong hashing (bcrypt or pgcrypto).
- Role-based access control for hosts and admins.
- Data validation at API and DB layer.

---

> ✅ This specification supports a secure, scalable, and well-documented RESTful backend architecture for the ALX Airbnb Clone project.

---
### 🎨 Designed By  
**Franklin Zyambo**  
*Cloud Architect | Data Analyst | Software Engineer*
