# tayara marketplace apis

## Categories

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

#### Category details

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
  

##### Error Responses

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
  

##### Example Curl Request

```bash
curl 'https://marketplace-api.tayara.tn/category/60be84be50ab95b45b08a0a5' \
--header 'Authorization: Bearer <APP_TOKEN>'
```

# AD management

## upload ad 's image

- **URL**
  
  https://marketplace-api.tayara.tn/upload
  
- **Method:**
  
  `POST`
  
- **URL Params**
  None
  
- **Data Params**
  

```
  file : form-data
```

- **Header Params**
  
  ```
  Authorization : Bearer < TOKEN >
  ```
  

- **Success Response:**
  
  - **Code:** 200 <br />
    **Content:**
    
    ```
     [ string ]  // array of images 's url
    ```
    

- **Error Response:**
  - **Code:** 404 NOT FOUND <br />
    **Content:**

```
     {   code:  404,
         error:  "Not found",
         message:  "Requested route was not found",}
```

OR

- **Code:** 401 UNAUTHORIZED <br />
  **Content:**
  
  ```
   {code:  401,
    error:  "Forbidden",
    message:  "You are forbidden to access .",}
  ```
  
  OR
  
- **Code:** 500 UNKNOW <br />
  **Content:**
  
  ```
    {code:  500,
     error:  "unknow",
     message:  "",}  // any other exeption
  ```
  

- **Sample Call:**

```
    curl --location --request POST 'https://marketplace-api.tayara.tn/upload' \
    --header 'Authorization: Bearer <Token>' \
    --form 'file=@"/home/tayara/Images/Capture d’écran de 2021-10-23 23-41-16.png"'         
```

## create Ad

- **URL**
  
  https://marketplace-api.tayara.tn/postad
  
- **Method:**
  
  `POST`
  
- **URL Params**
  None
  
- **Data Params**
  

```
  {
       "userid": string,                              // user 's id 
       "title": "test",                                  // title of  new    ad
       "subcategoryid":string                  // id of category  ( imported from category api )
       "description": "test new ad",         // description of new ad
       "images": string[],                            // array of images 's urls (  api upload image)
       "location": { 
            "latitude": double,                     //current user 's latitude
            "longitude": double ,                    //current user 's longitude
            "radius" : double  },                       
       "price": double,                                  // ad 's proposal price
       "adparamvalues": [ {                           // ad criteria
               "name": string,                            // those params must be imported from category 's api 
               "value":string                               //  name : name of param ; value : value of param
            } ], 
        "userphonenumber":string              //  phone number of ad 's owner

        "producttype": int                            //  0 : if ad is used , 1 : if ad is new
    }
```

- **Header Params**
  
  ```
  content-type: "application/json"
  Authorization : Bearer < TOKEN >
  ```
  

- **Success Response:**
  
  - **Code:** 200 <br />
    **Content:**
    
    ```
     { message  : "ad created successfully"    //  "ad was created ",
       id : ""                 // id of new ad ,
       code : 200      }`
    ```
    

- **Error Response:**
  - **Code:** 404 NOT FOUND <br />
    **Content:**

```
    {code:  404,
     error:  "Not found",
     message:  "Requested route was not found",}
```

OR

- **Code:** 401 UNAUTHORIZED <br />
  **Content:**
  
  ```
   {code:  401,
    error:  "Forbidden",
    message:  "You are forbidden to access .",}
  ```
  
  OR
  
- **Code:** 500 UNKNOW <br />
  **Content:**
  
  ```
   {code:  500,
    error:  "unknow",
    message:  "",}  // any other exeption
  ```
  

- **Sample Call:**
  
  ```
    curl --location --request POST 'https://marketplace-api.tayara.tn/postad' \
    --header 'Authorization: Bearer mehdites' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "userid": "ced8e24d-055e-4886-960b-d8da91323784",
        "title": "test",
        "subcategoryid": "60be84be50ab95b45b08a0a4",
        "description": "test new ad",
        "images": [
            "https://storage.googleapis.com/tayara-migration-yams-pro/29/297fa986-51dd-4e99-ac9f-243b55f5f48b"
        ],
        "location": {
                "latitude": 36.8468805,
                "longitude": 10.255426 ,
                "radius" : 10        
        },
        "price": 548.0,
        "adparamvalues": [
            { "name": "Kilométrage",  
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
