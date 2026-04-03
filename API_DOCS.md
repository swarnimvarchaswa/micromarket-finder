# Micromarket Finder API Documentation

This document explains how external applications can use the Micromarket Finder API to get the micromarket and zone for a specific set of geographical coordinates.

## Endpoint: `/api/find`

This is the primary endpoint to query location data. It accepts both `GET` and `POST` HTTP requests.

### 1. Using GET Request

The easiest way to hit the API is by appending the coordinates to the URL query string. 

**URL:**
```http
GET https://micromarket-finder.vercel.app/api/find?lat={latitude}&lon={longitude}
```

**Parameters:**
* `lat` or `latitude` - (Required) Latitude coordinate as a decimal number
* `lon` or `longitude` - (Required) Longitude coordinate as a decimal number

**Example (Curl):**
```bash
curl "https://micromarket-finder.vercel.app/api/find?lat=12.905143&lon=77.651003"
```

**Example (JavaScript Fetch):**
```javascript
fetch('https://micromarket-finder.vercel.app/api/find?lat=12.905143&lon=77.651003')
  .then(response => response.json())
  .then(data => console.log(data));
```

### 2. Using POST Request

If you prefer sending a payload, you can perform a POST request. The server accepts `application/json` as well as standard `application/x-www-form-urlencoded` forms.

**URL:**
```http
POST https://micromarket-finder.vercel.app/api/find
```

**Example JSON Payload:**
```json
{
  "lat": 12.905143,
  "lon": 77.651003
}
```

## Response Format

The API responds with JSON data.

**Success Response (HTTP 200)**
If the coordinates fall within recognized boundaries:
```json
{
  "found": true,
  "latitude": 12.905143,
  "longitude": 77.651003,
  "micromarket": "HSR Layout",
  "zone": "East"
}
```

**Not Found Response (HTTP 404)**
If the location does not fall inside any registered zones:
```json
{
  "found": false,
  "error": "Coordinates not found in any known micromarket",
  "latitude": 12.00000,
  "longitude": 77.00000
}
```

**Error Response (HTTP 400)**
If parameters are missing or invalid:
```json
{
  "error": "Please provide 'lat' and 'lon' parameters"
}
```
