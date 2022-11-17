# Tayara marketplace API documentation

## Categories

### get list of categories

#### get all categories

##### Request

`GET` https://marketplace-api.tayara.tn/categories

- **Headers:**
  
  ```yaml
  Authorization: "Bearer <APP_TOKEN>"
  ```
  

##### Success Response

- **Status:** `200 OK` 
  **Body:**
  
  ```json
  [
    {
      "id": "string",                  // id of current category
      "parentcategoryxid": "string",   // id of parent category
      "name": "string",                // name of category
    }
  ]
  ```
  

##### Error Responses

- **Status:** `404 NOT FOUND`**Body:**
  
  ```json
  {
      "code": 404,
      "error": "Not found",
      "message": "Requested route was not found"
  }
  ```
  

- **Status:** `401 UNAUTHORIZED`
  **Body:**
  
  ```json
  {
      "code": 401,
      "error": "Forbidden",
      "message": "You are forbidden to access ."
  }
  ```
  

##### Example Curl Request

```bash
curl 'https://marketplace-api.tayara.tn/categories' \
--header 'Authorization: Bearer <APP_TOKEN>'
```

#### Category details

##### Request

`GET` https://marketplace-api.tayara.tn/category/

- **Headers:**
  
  ```yaml
  Authorization: "Bearer <APP_TOKEN>"
  ```
  

##### Success Response

- **Status:** `200 OK`**Body:**
  
  ```json
  {
    "id": "string",                   // id of category
    "name": "string",
    "parentcategoryxid": "string",
    "adparams": [
      {
        "name": "string",             // name of param
        "type": "number",             // type of param:( "number" : range , "array" : select )
        "label": "string",            //label of param
        "possiblevalues": "string[]", // if type = "array"  :  possiblevalues = options in select box,
        "rangeValues": {              // if type = "number"  :  possiblevalues = limit of range
          "min": 0.0,                 // value min of range
          "max": 1000000.0,           // value max of range,
          "dependantName": ""         // if current parent is depends of other param (  model param of a car is depend of marque )
        }
      }
    ]
  }
  ```
  

##### Error Responses

- **Status:** `404 NOT FOUND`**Body:**
  
  ```json
  {
      "code": 404,
      "error": "Not found",
      "message": "Requested route was not found"
  }
  ```
  

- **Status:** `401 UNAUTHORIZED` **Body:**
  
  ```json
  {
      "code": 401,
      "error": "Forbidden",
      "message": "You are forbidden to access ."
  }
  ```
  
- **Status:** `500 UNKNOWN`
  
  **Body:**
  
  ```json
  {
      "code": 500,
      "error": "Unknown",
      "message": ""         // exception details
  }
  ```
  

##### Example Curl Request

```bash
curl 'https://marketplace-api.tayara.tn/category/60be84be50ab95b45b08a0a5' \
--header 'Authorization: Bearer <APP_TOKEN>'
```

## Ad Insertion

### Upload image

`POST` https://marketplace-api.tayara.tn/upload

- **Headers:**
  
  ```yaml
  Content-Type: "multipart/form-data"
  Authorization: "Bearer <APP_TOKEN>"
  ```
  

- **Body:**
  
  ```yaml
  file: <FILE_BLOB>
  ```
  

##### Success Response

- **Status:** `200 OK`
  
  **Body:**
  
  ```json
  {
    "id": "string",                   // id of category
    "name": "string",
    "parentcategoryxid": "string",
    "adparams": [
      {
        "name": "string",             // name of param
        "type": "number",             // type of param:( "number" : range , "array" : select )
        "label": "string",            //label of param
        "possiblevalues": "string[]", // if type = "array"  :  possiblevalues = options in select box,
        "rangeValues": {              // if type = "number"  :  possiblevalues = limit of range
          "min": 0.0,                 // value min of range
          "max": 1000000.0,           // value max of range,
          "dependantName": ""         // if current parent is depends of other param (  model param of a car is depend of marque )
        }
      }
    ]
  }
  ```
  

##### Error Responses

- **Status:** `404 NOT FOUND`
  
  **Body:**
  
  ```json
  {
      "code": 404,
      "error": "Not found",
      "message": "Requested route was not found"
  }
  ```
  

- **Status:** `401 UNAUTHORIZED`
  
  **Body:**
  
  ```json
  {
      "code": 401,
      "error": "Forbidden",
      "message": "You are forbidden to access ."
  }
  ```
  
- **Status:** `500 UNKNOWN`
  
  **Body:**
  
  ```json
  {
      "code": 500,
      "error": "Unknown",
      "message": ""         // exception details
  }
  ```
  

##### Example Curl Request

```bash
curl --X POST 'https://marketplace-api.tayara.tn/upload' \
--header 'Authorization: Bearer <Token>' \
--form 'file=@"/home/tayara/images/listing-image.png"'
```

### Upload image by url

`POST` https://marketplace-api.tayara.tn/upload-from-url

- **Headers:**

  ```yaml
  Content-Type: "application/json"
  Authorization: "Bearer <APP_TOKEN>"
  ```


- **Body:**

  ```json
  [
    "URL1",
    "URL2"
  ]
  ```


##### Success Response

- **Status:** `201 Created`

  **Body:**

  ```json
  [
    "image_url_on_tayara_servers",
    "image_url_on_tayara_servers"
  ]
  ```


##### Error Responses

- **Status:** `404 NOT FOUND`

  **Body:**

  ```json
  {
      "code": 404,
      "error": "Not found",
      "message": "Requested route was not found"
  }
  ```


- **Status:** `401 UNAUTHORIZED`

  **Body:**

  ```json
  {
      "code": 401,
      "error": "Forbidden",
      "message": "You are forbidden to access ."
  }
  ```

- **Status:** `500 UNKNOWN`

  **Body:**

  ```json
  {
      "code": 500,
      "error": "Unknown",
      "message": ""         // exception details
  }
  ```


##### Example Curl Request

```bash
curl --X POST 'https://marketplace-api.tayara.tn/upload' \
--header 'Authorization: Bearer <Token>' \
--data-raw '[
    "https://res.cloudinary.com/dtpgi0zck/image/upload/s--6vkGBwaH--/c_fit,h_580,w_860/v1/EducationHub/photos/floating-in-the-sea.jpg",
    "https://cdn.britannica.com/79/65379-050-5CF52BAC/Shortfin-mako-shark-seas.jpg"
]'
```

## Create Ad

`POST` https://marketplace-api.tayara.tn/postad

- **Headers**
  
  ```yaml
  Content-Type: "application/json"
  Authorization : "Bearer <APP_TOKEN>"
  ```
  
- **Body**
  
  ```json
  {
    "userid": "string",           // user's id 
    "title": "string",            // title of new ad
    "subcategoryid": "string",    // id of category ( imported from category api )
    "description": "string",      // description of new ad
    "images": [
      "string"                    // image url returned from the "image upload" endpoint
    ],
    "location": {
      "latitude": "double",       // current user's latitude
      "longitude": "double",      // current user's longitude
      "radius": "double"          // the accuracy in Meters of the geo-location provided
    },
    "price": "double",            // ad 's proposal price
    "adparamvalues": [
      {                           // ad criteria
        "name": "string",         // those params must be imported from category 's api 
        "value": "string"         //  name : name of param ; value : value of param
      }
    ],
    "userphonenumber": "string",  // phone number of ad 's owner
    "producttype": "int"          //  0: ad is used | 1: ad is new
  }
  ```
  

##### Success Response

- **Status:** `200 OK`
  
  **Body:**
  
  ```json
  {
    "code": 200,
    "message": "ad created successfully",
    "id": "string"  // id of newly inserted ad
  
  }
  ```
  

##### Error Responses

- **Status:** `404 NOT FOUND`
  
  **Body:**
  
  ```json
  {
      "code": 404,
      "error": "Not found",
      "message": "Requested route was not found"
  }
  ```
  

- **Status:** `401 UNAUTHORIZED`
  
  **Body:**
  
  ```json
  {
      "code": 401,
      "error": "Forbidden",
      "message": "You are forbidden to access ."
  }
  ```
  
- **Status:** `500 UNKNOWN`
  
  **Body:**
  
  ```json
  {
      "code": 500,
      "error": "Unknown",
      "message": ""         // exception details
  }
  ```
  

##### Example Curl Request

```bash
  curl --location --request POST 'https://marketplace-api.tayara.tn/postad' \
  --header 'Authorization: Bearer <APP_TOKEN>' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "userid": "ced8e24d-055e-4886-960b-d8da91323784",
  "title": "test",
  "subcategoryid": "60be84be50ab95b45b08a0a4",
  "description": "test new ad",
  "images": [
    "https://storage.googleapis.com/tayara-migration-yams-pro/29/297fa986-51dd-4e99-ac9f-243b55f5f48b",
    "https://storage.googleapis.com/tayara-migration-yams-pro/29/297fa986-51dd-4e99-ad8f-48Vb8997ff5a"
  ],
  "location": {
    "latitude": 36.8468805,
    "longitude": 10.255426,
    "radius": 100
  },
  "price": 548.0,
  "adparamvalues": [
    {
      "name": "Kilométrage",
      "value": "85"
    },
    {
      "name": "Couleur du véhicule",
      "value": "Camel"
    }
  ],
  "userphonenumber": "+21654896476",
  "producttype": 0
}'
```
# Tayara marketplace API Postman collection
In addition to this documentation, You can use Postman collection available [here](https://docs.api.tayara.tn/assets/tayara_marketplace_api.postman_collection.json).