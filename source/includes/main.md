# Overview - RideMyWay API

Welcome to the Ride-My-Way API documentation: You can use the API to access Ride My Way API endpoints, which can signup new users, sigin registered users, create a ride offer, request to join a ride offer, and respond to to a ride request.

This is a node/express application

`BASE API URL:` `https://emmaadesile-ridemyway.herokuapp.com`

This API supports CRUD operations: `POST`, `GET`, `PUT`, and `DELETE`

# Requests

An authorisation token is required to access all endpoints except `signup` and `signin` endpoints. You need to sign up, then login to get a token.

The token is passed in `req.headers`

`token`: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1MzIxMzA1NjIsImV4cCI6MTUzMjIxNjk2Mn0.dfDX0b5Z172HvizzxPlafsVpqd_KjhKjMRpzifctlIQ`

<aside class="notice">
You must replace <code>eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1MzIxMzA1NjIsImV4cCI6MTUzMjIxNjk2Mn0.dfDX0b5Z172HvizzxPlafsVpqd_KjhKjMRpzifctlIQ</code> with your auth token.
</aside>


# Users

## User signup

Creates a new user

> Request Body

```json
{
  "firstname": "John",
  "lastname": "Snow",
  "username": "johnsnow",
  "email": "johnsnow@gmail.com",
  "password": "gameofthrones",
  "confirmPassword": "gameofthrones"
}
```
> Response Body

```json
{
  "status": "success",
  "message": "Signup successful",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1MzIxMzA1NjIsImV4cCI6MTUzMjIxNjk2Mn0.dfDX0b5Z172HvizzxPlafsVpqd_KjhKjMRpzifctlIQ"
}
```

### HTTP Request

- Endpoint: `/auth/signup`
- Verb: `POST`
- Body: `application/x-www-form-urlencoded`

### HTTP Response

- Status: `201 - created`
- Body: `application/json`


## User signin

Signs in a registered user

> Request Body

```json
{
  "email": "johnsnow@gmail.com",
  "password": "gameofthrones",
}
```
> Response Body

```json
{
  "status": "success",
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1MzIxMzA1NjIsImV4cCI6MTUzMjIxNjk2Mn0.dfDX0b5Z172HvizzxPlafsVpqd_KjhKjMRpzifctlIQ"
}
```

### HTTP Request

- Endpoint: `/auth/signin`
- Verb: `POST`
- Body: `application/x-www-form-urlencoded`

### HTTP Response

- Status: `200`
- Body: `application/json`


# Rides

## Get all ride offers

This endpoint gets all available ride offers

> Response Body

```json
{
    "status": "Success",
    "rides": [
        {
            "ride_id": 1,
            "user_id": 2,
            "location": "Ikoyi",
            "destination": "Ajah",
            "departuretime": "19:00:00",
            "datecreated": "2018-07-14T23:00:00.000Z",
            "seatsavailable": 8
        },
        {
            "ride_id": 2,
            "user_id": 1,
            "location": "Ikorodu",
            "destination": "Maryland",
            "departuretime": "07:00:00",
            "datecreated": "2018-07-20T23:00:00.000Z",
            "seatsavailable": 5
        },
        {
            "ride_id": 3,
            "user_id": 1,
            "location": "CMS",
            "destination": "Ikeja",
            "departuretime": "13:00:00",
            "datecreated": "2018-07-20T23:00:00.000Z",
            "seatsavailable": 10
        }
    ]
}
```

### HTTP Request

- Endpoint: `/rides`
- Verb: `GET`

### HTTP Response

- Status: `/rides`
- Body: `application/json`


## Get a ride

This endpoint get a specific ride

> Response Body

```json
{
    "status": "Success",
    "ride": [
        {
            "ride_id": 1,
            "user_id": 2,
            "location": "Ikoyi",
            "destination": "Ajah",
            "departuretime": "19:00:00",
            "datecreated": "2018-07-14T23:00:00.000Z",
            "seatsavailable": 8
        }
    ]
}

```

### HTTP Request

- Endpoint: `/rides/:rideId`
- Verb: `GET`

### HTTP Response

- Status: `200 - ok`
- Body: `application/json`


## Create a ride

This endpoint create a ride offer

> Request Body

```json
{
  "location": "Yaba",
  "destination": "Ikeja",
  "departuretime": "13:00",
  "datecreated": "2018-07-20",
  "seatsavailable": "10",

}
```

> Response Body

```
{
    "status": "Success",
    "message": "Ride offer successfully created"
}
```

### HTTP Request

- Endpoint: `/users/rides`
- Verb: `POST`

### HTTP Response

- Status: `201 - created`
- Body: `application/json`


## Request to join a ride

This endpoint sends a request to join a ride offer

> Response Body

```json
{
    "status": "Success",
    "message": "Request to join ride offer pending approval from ride owner"
}
```

### HTTP Request

- Endpoint: `/rides/:rideId/requests`
- Verb: `POST`

### HTTP Response

- Status: `201 `
- Body: `application/json`


## Accept or Reject a ride offer

With this endpoint, the ride owner can accept or reject a ride request

> Request Body

```json
{
  "requestStatus": "accepted"
}
```

> Response Body

```json
{
  "status": "success",
  "message": "The ride request has been successfully `requestStatus`"
}
```

### HTTP Request

- Endpoint: `/users/rides/:rideId/requests/:requestId`
- Verb: `PUT`

### HTTP Response

- Status: `200 - ok `
- Body: `application/json`

## Get all ride requests

This endpoint gets all the requests for a ride

> Response Body

```json
{
  "user_id": 2,
  "ride_id": 1,
  "request_id": 2,
  "request_status": "pending",
  "requester_name": "John Snow"
}
```

### HTTP Response

- Status: `200 - ok `
- Body: `application/json`