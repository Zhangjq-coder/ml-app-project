---
layout: default
title: API Documentation
---

# API Documentation

This API provides endpoints for interacting with the machine learning model.

## Base URL

```
https://your-app-url.com/api
```

## Endpoints

### Health Check

Check if the API is running.

**Endpoint**: `/health`

**Method**: `GET`

**Response**:
```json
{
  "status": "healthy",
  "timestamp": "2023-11-15T10:30:00Z"
}
```

### Predict

Make predictions using the trained model.

**Endpoint**: `/predict`

**Method**: `POST`

**Request Body**:
```json
{
  "features": [5.1, 3.5, 1.4, 0.2]
}
```

**Response**:
```json
{
  "prediction": "setosa",
  "confidence": 0.95,
  "class_probabilities": {
    "setosa": 0.95,
    "versicolor": 0.04,
    "virginica": 0.01
  }
}
```

### Model Information

Get information about the current model.

**Endpoint**: `/model/info`

**Method**: `GET`

**Response**:
```json
{
  "model_name": "iris_classifier",
  "model_version": "1.0.0",
  "model_type": "RandomForestClassifier",
  "training_date": "2023-11-15T10:30:00Z",
  "features": ["sepal_length", "sepal_width", "petal_length", "petal_width"],
  "target_classes": ["setosa", "versicolor", "virginica"],
  "accuracy": 0.97,
  "precision": 0.96,
  "recall": 0.97,
  "f1_score": 0.96
}
```

### Batch Predict

Make predictions for multiple data points.

**Endpoint**: `/predict/batch`

**Method**: `POST`

**Request Body**:
```json
{
  "features": [
    [5.1, 3.5, 1.4, 0.2],
    [6.2, 2.9, 4.3, 1.3],
    [7.7, 3.8, 6.7, 2.2]
  ]
}
```

**Response**:
```json
{
  "predictions": [
    {
      "prediction": "setosa",
      "confidence": 0.95
    },
    {
      "prediction": "versicolor",
      "confidence": 0.87
    },
    {
      "prediction": "virginica",
      "confidence": 0.92
    }
  ]
}
```

## Error Responses

### 400 Bad Request

```json
{
  "error": "Bad Request",
  "message": "Invalid input data",
  "details": "Features must be a list of 4 numeric values"
}
```

### 404 Not Found

```json
{
  "error": "Not Found",
  "message": "The requested endpoint does not exist"
}
```

### 500 Internal Server Error

```json
{
  "error": "Internal Server Error",
  "message": "An unexpected error occurred"
}
```

## Usage Examples

### Using curl

```bash
# Health check
curl -X GET https://your-app-url.com/api/health

# Make a prediction
curl -X POST https://your-app-url.com/api/predict \
  -H "Content-Type: application/json" \
  -d '{"features": [5.1, 3.5, 1.4, 0.2]}'

# Get model information
curl -X GET https://your-app-url.com/api/model/info
```

### Using Python requests

```python
import requests

# Health check
response = requests.get("https://your-app-url.com/api/health")
print(response.json())

# Make a prediction
data = {"features": [5.1, 3.5, 1.4, 0.2]}
response = requests.post(
    "https://your-app-url.com/api/predict",
    json=data
)
print(response.json())

# Get model information
response = requests.get("https://your-app-url.com/api/model/info")
print(response.json())
```

### Using JavaScript fetch

```javascript
// Health check
fetch("https://your-app-url.com/api/health")
  .then(response => response.json())
  .then(data => console.log(data));

// Make a prediction
fetch("https://your-app-url.com/api/predict", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    features: [5.1, 3.5, 1.4, 0.2]
  })
})
  .then(response => response.json())
  .then(data => console.log(data));

// Get model information
fetch("https://your-app-url.com/api/model/info")
  .then(response => response.json())
  .then(data => console.log(data));
```

## Rate Limiting

The API has a rate limit of 100 requests per minute per IP address. If you exceed this limit, you will receive a 429 Too Many Requests response.

## Authentication

Currently, the API does not require authentication. In a production environment, you should implement proper authentication and authorization mechanisms.

## Versioning

The API is versioned using URL paths. The current version is v1. Future versions will be available at `/api/v2`, `/api/v3`, etc.

## Testing

You can test the API using the following tools:

1. **Postman**: A popular API testing tool
2. **curl**: A command-line tool for making HTTP requests
3. **Python requests**: A Python library for making HTTP requests
4. **JavaScript fetch**: A browser API for making HTTP requests

## Support

If you encounter any issues with the API, please:

1. Check the error messages for details
2. Review this documentation for correct usage
3. Create an issue in the GitHub repository
4. Contact the development team

## Changelog

### v1.0.0 (2023-11-15)

- Initial release
- Added health check endpoint
- Added prediction endpoint
- Added model information endpoint
- Added batch prediction endpoint