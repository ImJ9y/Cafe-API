# ☕️ Cafe API

A RESTful API built with Flask for managing a cafe database. This API allows users to search, retrieve, add, update, and delete cafe information.

---

## ✨ Features

- 🌍 Search cafes by location
- 📃 Get all cafes
- 🌟 Retrieve a random cafe
- ➕ Add new cafes
- 💸 Update cafe coffee prices
- ❌ Delete cafes (requires API key)

---

## ⚙️ Prerequisites

- Python 3.7+
- pip (Python package manager)

---

## 📦 Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd cafe-api
```

2. Install dependencies:
- On Windows:
```bash
python -m pip install -r requirements.txt
```
- On macOS/Linux:
```bash
pip3 install -r requirements.txt
```

---

## 🔧 Configuration

- Uses SQLite. A `cafes.db` file is automatically created on first run.

---

## 🌐 Running the Application

```bash
python main.py
```

- Default server: [http://localhost:5000](http://localhost:5000)

---

## 🚀 API Endpoints

### `GET /`
Returns the home page.

---

### `GET /random`
Returns a random cafe.
```json
{
  "cafe": {
    "id": 1,
    "name": "Lighthaus",
    "map_url": "https://g.page/thelighthaus?share",
    "img_url": "https://example.com/image.jpg",
    "location": "Chelsea",
    "seats": "20-30",
    "has_toilet": true,
    "has_wifi": true,
    "has_sockets": true,
    "can_take_calls": true,
    "coffee_price": "£2.80"
  }
}
```

---

### `GET /all`
Returns all cafes.
```json
{
  "all_cafes": [
    {
      "id": 1,
      "name": "Lighthaus",
      ...
    },
    ...
  ]
}
```

---

### `GET /search?loc=LOCATION`
Search cafes by location.

#### Success:
```json
{
  "cafe": {
    "id": 2,
    "name": "Peckham Cafe",
    ...
  }
}
```
#### Not Found:
```json
{
  "error": {
    "Not Found": "Sorry, we don't have a cafe at that location."
  }
}
```

---

### `POST /add`
Add a new cafe. (form-data)

Required fields:
- name, map_url, img_url, loc, seats, toilet, wifi, sockets, calls

Optional:
- coffee_price

#### Success:
```json
{
  "response": {
    "success": "Successfully added the new cafe."
  }
}
```

---

### `PATCH /update-price/<cafe_id>?new_price=VALUE`
Update coffee price of a specific cafe.

#### Success:
```json
{
  "response": {
    "success": "Successfully updated the price."
  }
}
```
#### Not Found:
```json
{
  "error": {
    "Not Found": "Sorry a cafe with that id was not found in the database."
  }
}
```

---

### `DELETE /report-closed/<cafe_id>?api-key=TopSecretAPIKey`
Delete a cafe. Requires API key.

#### Success:
```json
{
  "response": {
    "success": "Successfully deleted the cafe."
  }
}
```
#### Unauthorized:
```json
{
  "error": {
    "Unauthorized": "Sorry, that's not allowed. Make sure you have the correct api_key."
  }
}
```
#### Not Found:
```json
{
  "error": {
    "Not Found": "Sorry, a cafe with that id was not found in the database."
  }
}
```

---

## 📊 Database Schema

| Field             | Type          | Description                        |
|------------------|---------------|------------------------------------|
| `id`             | Integer       | Primary key                        |
| `name`           | String(250)   | Cafe name (unique)                |
| `map_url`        | String(500)   | Google Maps URL                    |
| `img_url`        | String(500)   | Image URL                          |
| `location`       | String(250)   | Location                           |
| `seats`          | String(250)   | Number of seats                    |
| `has_toilet`     | Boolean       | Has toilet facilities              |
| `has_wifi`       | Boolean       | Has WiFi                           |
| `has_sockets`    | Boolean       | Has power sockets                  |
| `can_take_calls` | Boolean       | Suitable for calls                 |
| `coffee_price`   | String(250)   | Coffee price (optional)            |

---

## 🔮 Testing the API

### cURL:
```bash
# Get all cafes
curl http://localhost:5000/all

# Search for a cafe
curl http://localhost:5000/search?loc=Chelsea

# Add a cafe
curl -X POST http://localhost:5000/add \
  -F "name=New Cafe" \
  -F "map_url=https://maps.google.com/..." \
  -F "img_url=https://example.com/image.jpg" \
  -F "loc=London" \
  -F "seats=30" \
  -F "toilet=true" \
  -F "wifi=true" \
  -F "sockets=true" \
  -F "calls=false" \
  -F "coffee_price=£3.00"
```

### Postman:
Import and test endpoints visually.

### Python Requests:
```python
import requests
response = requests.get("http://localhost:5000/all")
print(response.json())
```

---

## 🔒 Error Handling

- 200: Success
- 201: Created
- 403: Forbidden (Invalid API key)
- 404: Not Found

---

## ⚠️ Security Notes

- API key is hardcoded as `TopSecretAPIKey`
- Use environment variables for secrets
- Add proper authentication & validation in production

---

## ✨ Future Improvements

- Input validation for all fields
- JWT authentication
- Pagination for `/all`
- Full cafe update endpoint
- Advanced filtering options
- Rate limiting
- Unit and integration tests

---

## 📅 License

[License]

---

## 👥 Contact

**Jay Im**

---
