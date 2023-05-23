# Accounts Endpoint

The Accounts Endpoint allows you to mange user accounts for the applications. Below are the endpoints avaiable:

| HTTP Request | Endpoints | Purpose of the Endpoint |
|--------------|-----------|-------------------------|
| PUT | /accounts | Create an user account |
| GET | /accounts | Get details of all user accounts |
| GET | /accounts/{id} | Get details of a specific account |
| POST | /accounts/{account.uid}/toggle | Enable / Disable a specific account |
| PATCH | /accounts/{account.uid} | Update an account |
| DELETE | /accounts/{uid} | Delete a specific account |


## How to create an Account

Pre-Requisites: 

1. You need valid user credentials for the applications to obtain token (Refer [here](https://recasta.github.io/docs/#/REST/GenerateToken#how-to-obtain-the-token) on how to generate a token)

Steps:

1. REST Request Details for Creating an Account
   
   - REST Endpoint: **<URL>/accounts**
   > URL is the domain for the environment E.g. console.recasta.dummy
   - Request Type: **PUT**
   - Request Header: **Content-Type: application/json**
   - Request Header: **Authorization: bearer Authentication_Token**
   - Request Body: **Content in JSON format**

Request Body Format:
```
{
  "account": {
    "title": "TEST-ACCOUNT-USERNAME",
    "enabled": false
  },
  "namespace": "Namespace ID",
  "credentials": {
    "type": "standard",
    "data": [
      "TEST-ACCOUNT-USERNAME",
      "PASSWORD"
    ]
  }
}
```

2. Once the above REST Request is send with the required JSON body to the endpoint, an account will be created and JSON response will be send back.

Sample Response:
```
{
    "account": {
        "uuid": "8815bce8-9b99-433e-ac5d-c8932e7c70c9",
        "title": "TEST-ACCOUNT-USERNAME",
        "enabled": false,
        "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8"
    }
}
```

## How to get all Accounts data

Pre-Requisites: 

1. You need valid user credentials for the applications to obtain token (Refer [here](https://recasta.github.io/docs/#/REST/GenerateToken#how-to-obtain-the-token) on how to generate a token)
2. You need a namespace 

Steps:

1. REST Request Details for Getting all Accounts
   
   - REST Endpoint: **<URL>/accounts**
   > URL is the domain for the environment E.g. console.recasta.dummy
   - Request Type: **GET**
   - Request Header: **Authorization: bearer Authentication_Token**

2. Once the above REST Request is send to the endpoint, it returns all the accounts present. If the user is admin then all accounts manged by the Admin will be returned otherwise only the self account will be returned.

Response Format:
```
{
    "accounts": [
        {
            "uuid": "11d31fa7-969c-474d-80cc-d097c78324b1",
            "title": "TEST-ACCOUNT-USERNAME",
            "enabled": true,
            "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
            "access": {
                "level": "ROOT",
                "role": "OWNER",
                "namespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
            }
        },
        ...
}
```

## How to get an Account data

Pre-Requisites: 

1. You need valid user credentials for the applications to obtain token (Refer [here](https://recasta.github.io/docs/#/REST/GenerateToken#how-to-obtain-the-token) on how to generate a token)
2. You need a namespace

Steps:

1. REST Request Details for getting a namespace data
   
   - REST Endpoint: **<URL>/accounts/{id}**
   > URL is the domain for the environment E.g. console.recasta.dummy
   - Request Path Parameters: **id should be a valid account id**
   - Request Type: **GET**
   - Request Header: **Authorization: bearer Authentication_Token**

2. Once the above REST Request is send with the required path parameters to the endpoint, if the account id is valid then the account details in JSON response will be send back.

Response Format:
```
{
    "uuid": "ID",
    "title": "TEST-ACCOUNT-USERNAME",
    "enabled": false,
    "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
    "access": {
        "level": "ADMIN",
        "role": "OWNER",
        "namespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8"
    }
}
```


## How to enable/disable an Account

Pre-Requisites:

1. You need valid user credentials for the applications to obtain token (Refer [here](https://recasta.github.io/docs/#/REST/GenerateToken#how-to-obtain-the-token) on how to generate a token)
2. You have created a new user that is currently disabled 

Steps:

1. REST Request Details for getting a namespace data
   
   - REST Endpoint: **<URL>/accounts/{id}/toggle**
   > URL is the domain for the environment E.g. console.recasta.dummy
   - Request Path Parameters: **id should be a valid account id**
   - Request Type: **POST**
   - Request Header: **Authorization: bearer Authentication_Token**

Request Body Format:
```
{
  "enabled": true,
  "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
  "access": {
    "level": "ADMIN",
    "role": "OWNER",
    "namespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8"
  }
}
```

2. Once the above REST Request is send with the required JSON body to the endpoint, an account will be created and JSON response will be send back.

Sample Response:
```
{
    "uuid": "8815bce8-9b99-433e-ac5d-c8932e7c70c9",
    "title": "TEST-ACCOUNT-USERNAME",
    "enabled": false,
    "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
    "access": {
        "level": "ADMIN",
        "role": "OWNER",
        "namespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8"
    }
}
```


## How to update an Account

Pre-Requisites: 

1. You need valid user credentials for the applications to obtain token (Refer [here](https://recasta.github.io/docs/#/REST/GenerateToken#how-to-obtain-the-token) on how to generate a token)
2. You need a namespace 

Steps:

1. REST Request Details for Updating an Account
   
   - REST Endpoint: **<URL>/accounts/{account.uid}**
   > URL is the domain for the environment E.g. console.recasta.dummy
   - Request Path Parameters: **account.uid should be a valid account id**
   - Request Type: **PATCH**
   - Request Header: **Content-Type: application/json**
   - Request Header: **Authorization: bearer Authentication_Token**
   - Request Body: **Content in JSON format**

Request Body Format:
```
{
  "title": "TEST-ACCOUNT-USERNAME",
  "enabled": true,
  "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
    "access": {
        "level": "ADMIN",
        "role": "OWNER",
        "namespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8"
    }
}
```

Sample Request Body:

Below is an example of an update JSON request which will update the account with ID 0x000. The fields it will update are Name, Password and Enabled.
```
{
    "uuid": "0x000",
    "title": "TEST-ACCOUNT-USERNAME",
    "enabled": true,
    "defaultNamespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8",
    "access": {
        "level": "ADMIN",
        "role": "OWNER",
        "namespace": "a1401aaa-bf1e-4847-af8b-e581c46db2f8"
    }
}
```

2. Once the above REST Request is send with the required JSON body to the endpoint, an HTTP 200 reposne is receive if the namespace update was successful. Otherwise you will get an error with the reason why the update was not successful.

## How to delete an Account   

Pre-Requisites: 

1. You need valid user credentials for the applications to obtain token (Refer [here](https://recasta.github.io/docs/#/REST/GenerateToken#how-to-obtain-the-token) on how to generate a token)
2. You need a namespace 

Steps:

1. REST Request Details for Deleting an Account
   
   - REST Endpoint: **<URL>/accounts/{uid}**
   > URL is the domain for the environment E.g. console.recasta.dummy
   - Request Path Parameters: **uid should be a valid account id in recasta**
   - Request Type: **DELETE**
   - Request Header: **Authorization: bearer Authentication_Token**

2. Once the above REST Request is send with the required path parameters to the endpoint, an HTTP 200 reposne is receive if the account is deleted. Otherwise you will get an error with the reason why the request was not successful.
