Day 2

# **E-Commerce Furniture Website**  

This project is a modern e-commerce platform that offers trendy, Pinterest-inspired, and budget-friendly furniture. Built with `Next.js 15` and `Tailwind CSS`, it integrates `Sanity` for data management. The system includes both `user` and `admin` functionalities, such as managing products, tracking shipments, processing orders, and more.  

---  

## **API Overview**  

This document provides details on the API specifications for the system. Below are the key APIs implemented:  

- **Products API**: Fetches product details.  
- **Shipment API**: Handles shipments, including creation, tracking, and real-time updates.  

---  

### **1. Products API**  

#### **Endpoint:** `/api/products`  
**Method:** `GET`  

Retrieves a list of available products.  

##### **Request**  
- No request body is required.  

##### **Response**  
Returns an array of product objects with details such as name, description, price, stock quantity, and image.  

```json
[
  {
    "id": "123",
    "name": "Modern Sofa",
    "description": "A stylish, modern sofa for your living room.",
    "price": 599.99,
    "image": "https://example.com/images/sofa.jpg",
    "category": "Sofas",
    "stock": 50
  }
]
```  

---  

### **2. Shipment API**  

#### **My Endpoint:** `/api/shipmentOrder`  
(Calls the `/api/shipments/` endpoint)  

#### **Shippo Endpoint:** `/api/shipments/`  
**Method:** `POST`  

Creates a shipment and retrieves a tracking number.  

##### **Request**  
Requires recipient and shipment details, including address, weight, and product ID.  

```json
{
  "sender": {
    "name": "E-commerce Store",
    "street1": "123 Store Lane",
    "city": "San Francisco",
    "state": "CA",
    "zip": "94107",
    "country": "US"
  },
  "recipient": {
    "name": "John Doe",
    "street1": "456 User Street",
    "city": "New York",
    "state": "NY",
    "zip": "10001",
    "country": "US"
  },
  "package": {
    "length": "10",
    "width": "10",
    "height": "10",
    "distance_unit": "in",
    "weight": "5",
    "mass_unit": "lb"
  }
}
```  

##### **Response**  
Returns tracking details, including shipment ID, tracking number, carrier, and estimated delivery time.  

```json
{
  "shipmentId": "987",
  "trackingNumber": "1234567890",
  "carrier": "shippo",
  "eta": "2025-01-18T10:00:00Z",
  "status": "In Transit"
}
```  

---  

### **3. Live Tracking API**  

#### **My Endpoint:** `/api/liveTracking`  
(Calls the `/api/tracks/{carrier}/{trackingNumber}` API)  

#### **Shippo Endpoint:** `/api/tracks/{carrier}/{trackingNumber}`  
**Method:** `GET`  

Fetches real-time tracking updates using the tracking number.  

##### **Request**  
- **URL Parameters:**  
  - `carrier`: The shipping provider (e.g., Shippo).  
  - `trackingNumber`: The tracking number retrieved from `/api/shipments/`.  

##### **Response**  
Returns live tracking updates, including ETA, status, tracking history, and location.  

```json
{
  "trackingNumber": "1234567890",
  "carrier": "shippo",
  "eta": "2025-01-18T10:00:00Z",
  "status": "In Transit",
  "trackingHistory": [
    {
      "date": "2025-01-16T10:00:00Z",
      "location": "New York, NY",
      "status": "Shipped"
    },
    {
      "date": "2025-01-17T14:00:00Z",
      "location": "Philadelphia, PA",
      "status": "In Transit"
    }
  ],
  "origin": {
    "city": "New York",
    "country": "US"
  },
  "destination": {
    "city": "Los Angeles",
    "country": "US"
  }
}
```  

---  

### **API Summary**  

- **`/api/products`** → Retrieves product details.  
- **`/api/shipments/`** → Creates shipments and provides tracking numbers.  
- **`/api/tracks/{carrier}/{trackingNumber}`** → Fetches real-time tracking updates.  

## **Full API Endpoints**  

| Endpoint | Method | Purpose |  
|----------|--------|---------|  
| `/api/create-order` | POST | Creates a new order |  
| `/api/orders` | GET | Fetches all orders (admin access) |  
| `/api/shipengine/create-label` | POST | Generates a shipping label |  
| `/api/shipengine/get-rates` | GET | Retrieves shipping rates |  
| `/api/shipengine/track-shipment` | GET | Tracks a shipment |  
| `/api/track-orders` | GET | Displays user orders |  
| `/api/send/confirmation-email` | POST | Sends order confirmation emails |  
| `/api/reviews/[productId]` | POST | Submits a product review |  
| `/api/reviews/[productId]` | GET | Fetches product reviews |  

---

