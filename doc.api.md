# Api Paymakuta ecommerce

## token

- There is how you can get a token from our server.
  > route : `/token`

```json
//method : POST
data : {
    "username" : "string",
    "password" : "string"
}

// response structure if success
{
    token : "string",
    refresh : "string"
}
```

- The way to refresh your token, for example, if it expires
  > route : `/token/refresh`

```json
// method : POST
data : {
    refresh : "string"
}

// response structure if success :
{
    token : "string"
}
```

---

## registration and authentication

- To register a new customer :

> routre : `/register`

```json
//method : POST
data : {
    "firstname" : "string",
    "lastname" : "string",
    "mail" : "string",
    "role" : "string",  // enum : ["customer", "carrier"]
    "gender" : "string", // enum : ["male", "female", "other"]
    "address" : {
        "city" : "string",
        "coutry" : "string",
        "level" : "string",
        "street" : "string",
        "zip" : "string"
    }
}

// reponse structure
{
    "status" : 201,
    "message" : "Customer create successfully",
    "data" : {
        "firstname" : "string",
        "lastname" : "string",
        "mail" : "string",
        "role" : "string",  // enum : ["customer", "carrier"]
        "gender" : "string", // enum : ["male", "female", "other"]
        "address" : {
            "city" : "string",
            "coutry" : "string",
            "level" : "string",
            "street" : "string",
            "zip" : "string"
        }
    }
}
```

- to login or authentifie a customer
  > route : `/auth`

```json
// method : POST
data : {
    "mail" : "string",
    "password" : "string"
}

// response structure if success
{
    "status" : 200,
    "message" : "custmer founded",
    "data" : {
        "firstname" : "string",
        "lastname" : "string",
        "mail" : "string",
        "role" : "string",  // enum : ["customer", "carrier"]
        "gender" : "string", // enum : ["male", "female", "other"]
        "address" : {
            "city" : "string",
            "coutry" : "string",
            "level" : "string",
            "street" : "string",
            "zip" : "string"
        },
        "active_oder" : [{
            "id": "string",
            "article": "string",
            "carrier": "string",
            "order_at": "date",
            "price_ht": "string",
            "price_ttc": "string",
            "status": "in_progress", // enum : ["on_hold", "closed", "canceled", ""]
            "tva": "string",
        }]
    }
}
```

---

## Manage articles

- get many articles and create one
  > route : `/articles`

```json
// action create an article
// method : POST
data : {
    "title" : "banana",
    "description" : "A bio production",
    "selling_price" : 0.4,
    "currency" : "USD", //enum ["USD", "CDF"]
    "size" : "18-21 cm",
    "stock_min" : 1,
    "weight" : 102,
    "weight_unit" : "g", //enum ["kg", "g"]
    "picture_url" : "http://woubou.com/picture/ueu6g77gfyueg6",
    "customer" : {
        "username" : "Tatsumi Makima",
        "customer_id" : 203
    },
    "category" : {
        "name" : "fruit",
        "description" : "bio type"
    }
}

// create article response structure if success

{
    "status" : 201,
    "message" : "article created successfully",
    "data" : {
        "id" : 203,
        "title" : "banana",
        "description" : "A bio production",
        "selling_price" : 0.4,
        "currency" : "USD", //enum ["USD", "CDF"]
        "size" : "18-21 cm",
        "stock_min" : 1,
        "weight" : 102,
        "weight_unit" : "g", //enum ["kg", "g"]
        "picture_url" : "http://woubou.com/picture/ueu6g77gfyueg6",
        "customer" : {
            "username" : "Tatsumi Makima",
            "customer_id" : 203
        },
        "category" : {
            "name" : "fruit",
            "description" : "bio type"
        }
    }
}

// action : get many article
// method : GET
data : {
    types : ["fruits", "computer"],
    limite : 20, // by default limit equals 20
}

// response structure if success
{
    "status" : 200,
    "message" : "data for articles which have the type fruits and computer",
    "data" : [{
        "id": 20,
        "create_at": "23 Mar 2023 10:45:00 GMT",
        "update_at": "01 Jun 2023 10:45:00 GMT",
        "title" : "banana",
        "description" : "A bio production",
        "selling_price" : 0.4,
        "currency" : "USD", //enum ["USD", "CDF"]
        "size" : "18-21 cm",
        "stock_min" : 1,
        "weight" : 102,
        "weight_unit" : "g", //enum ["kg", "g"]
        "picture_url" : "http://woubou.com/picture/ueu6g77gfyueg6",
        "customer" : {
            "username" : "Tatsumi Makima",
            "customer_id" : 203
        },
        "category" : {
            "name" : "fruit",
            "description" : "bio type"
        }
    }]
}
```

- Get one article and update one article

> route : `/article/:id`

```json
// action : update one article
// method : PUT
// note : this route is dynamic. Replace the ':id' by the proprety id.
data : {
    "title" : "banana",
    "description" : "A bio production",
    "selling_price" : 0.4,
    "currency" : "USD", //enum ["USD", "CDF"]
    "size" : "18-21 cm",
    "stock_min" : 1,
    "weight" : 102,
    "weight_unit" : "g", //enum ["kg", "g"]
    "picture_url" : "http://woubou.com/picture/ueu6g77gfyueg6",
    "category" : {
        "name" : "fruit",
        "description" : "bio type"
    },
    "customer" : {
        "username" : "Tatsumi Makima",
        "customer_id" : 203
    },
}

// update article response structure if success
{
    "status" : 200,
    "message" : "article updated with success"
}


// action : get one artcile
// method : GET
// note : data option is not required.

//response structure if success.
{
    "status" : 200,
    "message" : "data for articles which have the type fruits and computer",
    "data" : {
        "id": 20,
        "create_at": "23 Mar 2023 10:45:00 GMT",
        "update_at": "01 Jun 2023 10:45:00 GMT",
        "title" : "banana",
        "description" : "A bio production",
        "selling_price" : 0.4,
        "currency" : "USD", //enum ["USD", "CDF"]
        "size" : "18-21 cm",
        "stock_min" : 1,
        "weight" : 102,
        "weight_unit" : "g", //enum ["kg", "g"]
        "picture_url" : "http://woubou.com/picture/ueu6g77gfyueg6",
        "customer" : {
            "username" : "Tatsumi Makima",
            "customer_id" : 203
        },
        "category" : {
            "name" : "fruit",
            "description" : "bio type"
        }
    }
}
```

---

## manage orders

- create one order or get many order
  > route : `/orders`

```json
// action : pass a command or create an order
// method : POST
// note : can add many commands
data : {
    "articles" : [{
        "article_id": 20,
        "price_ht": 10.03,
        "price_ttc": 11.8,
        "tva": 0.19,
    }],
    "customer_id" : 302
}

// pass a command response structure if success
{
    "status" : 201,
    "message" : "order(s) saved with success",
}


// action : get many order
// method : GET
//
```

- 
