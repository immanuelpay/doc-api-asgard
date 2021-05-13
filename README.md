# ASGARD API Documentation
- Base URL : **`https://asgard-api.herokuapp.com/api`**
- Header : 
  - Accept: application/json


### Authentication (ADMIN)
- #### Register
    Request
    - Method: **POST**
    - Endpoint: **`/register`**
    - Header
      - Content-Type: application/json
    - Body
        Request | Rule
        -------- | ------
        name | required, string
        email | required, email
        password | required, string
        password_confirmation | required, same: password

    <br>
    Response
```json
{
    "status": "success",
    "user": {
        "name": "Example",
        "email": "example@mail.com",
        "updated_at": "2021-05-13T15:23:27.000000Z",
        "created_at": "2021-05-13T15:23:27.000000Z",
        "id": 2
    },
    "access_token": "example_token"
}
```

- #### Login
    Request
    - Method: **POST**
    - Endpoint: **`/login`**
    - Header
      - Content-Type: application/json
    - Body
        Request | Rule
        -------- | ------
        name | required, string
        email | required, email

    <br>
    Response
```json
{
    "status": "success",
    "user": {
        "id": 1,
        "name": "Example",
        "email": "example@mail.com",
        "email_verified_at": null,
        "status": "1",
        "created_at": "2021-05-13T13:29:57.000000Z",
        "updated_at": "2021-05-13T13:29:57.000000Z"
    },
    "access_token": "example_token"
}
```

- #### Logout (ADMIN)
    Request
    - Method: **POST**
    - Endpoint: **`/logout`**
    - Header
      - Authorization: **`Bearer ${token}`**

    <br>
    Response
```json
{
    "status": "success",
    "message": "You have been successfully logged out!"
}
```

### Event
- URL Image : **`https://asgard-api.herokuapp.com/images/events/`**
- #### All Event
    Request
    - Method: **GET**
    - Endpoint: **`/event`**

    <br>
    Response
```json
{
    "status": "success",
    "data": [
        {
            "id": 1,
            "name": "PMPL ID S5",
            "genre": "Tencent Gamming",
            "organizer": "PUBG INDONESIA",
            "slot": 20,
            "image": "pmpl_id_s5_1620914124.png",
            "price_pool": 20000000,
            "fee": 100000,
            "description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
            "detail": null,
            "address": null,
            "venue": "Kota Kupang",
            "status": "1",
            "date": "2021-05-20 00:00:00",
            "created_at": "2021-05-13T13:55:24.000000Z",
            "updated_at": "2021-05-13T13:55:24.000000Z"
        }
    ]
}
```

- #### Show Event
    Request
    - Method: **GET**
    - Endpoint: **`/event/{id}`**

    <br>
    Response
```json
{
    "status": "success",
    "data": [
        {
            "id": 1,
            "name": "PMPL ID S5",
            "genre": "Tencent Gamming",
            "organizer": "PUBG INDONESIA",
            "slot": 20,
            "image": "pmpl_id_s5_1620914124.png",
            "price_pool": 20000000,
            "fee": 100000,
            "description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
            "detail": null,
            "address": null,
            "venue": "Kota Kupang",
            "status": "1",
            "date": "2021-05-20 00:00:00",
            "created_at": "2021-05-13T13:55:24.000000Z",
            "updated_at": "2021-05-13T13:55:24.000000Z"
        }
    ]
}
```

- #### Add Event (ADMIN)
    Request
    - Method: **POST**
    - Endpoint: **`/event`**
    - Header
      - Content-Type: multipart/form-data
      - Authorization: **`Bearer ${token}`**
    - Body
        Request | Rule
        -------- | ------
        name | required, string
        genre | required, string
        organizer | required, string
        slot | required, numeric
        price_pool | required, double
        fee | required, double
        description | required, string
        venue | required, string
        date | required, date
        image | required, image

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully added"
}
```

- #### Edit Event (ADMIN)
    Request
    - Method: **POST**
    - Endpoint: **`/event/{id}`**
    - Header
      - Content-Type: multipart/form-data
      - Authorization: **`Bearer ${token}`**
    - Body
        Request | Rule
        -------- | ------
        name | required, string
        genre | required, string
        organizer | required, string
        slot | required, numeric
        price_pool | required, double
        fee | required, double
        description | required, string
        venue | required, string
        date | required, date
        image | nullable, image

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully updated"
}
```

- #### Delete Event (ADMIN)
    Request
    - Method: **DELETE**
    - Endpoint: **`/event/{id}`**
    - Header
      - Authorization: **`Bearer ${token}`**

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully deleted"
}
```

- #### Checkout Event
    Request
    - Method: **POST**
    - Endpoint: **`/event/{id}/checkout`**
    - Header
      - Content-Type: application/json
    - Body
        Request | Rule
        -------- | ------
        created_by | required, string
        name | required, string
        email | required, email
        team_name | required, string
        phone_number | required, string

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully added, please make a payment and upload proof of payment"
}
```

- #### Upload Proof of Payment
    Request
    - Method: **POST**
    - Endpoint: **`/transaction/{uuid}/bukti-pembayaran`**
    - Header
      - Content-Type: multipart/form-data
    - Body
        Request | Rule
        -------- | ------
        bukti_pembayaran | required, image, max: 512kb

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully uploaded, please wait for admin verification!"
}
```

<br>
### Transaction
- URL Image : **`https://asgard-api.herokuapp.com/images/bukti_pembayaran/`**
- #### All Transaction
    Request
    - Method: **GET**
    - Endpoint: **`/transaction`**

    <br>
    Response
```json
{
    "status": "success",
    "data": [
        {
            "id": 1,
            "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
            "id_event": 2,
            "id_checkout_detail": 1,
            "id_bukti_bayar": 1,
            "created_by": null,
            "deleted_at": null,
            "created_at": "2021-05-13T14:41:11.000000Z",
            "updated_at": "2021-05-13T14:41:11.000000Z",
            "checkout_detail": {
                "id": 1,
                "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
                "name": "Imanuel Pay",
                "email": "imanuelpay@mail.com",
                "team_name": "SanSquad",
                "phone_number": "081234567890",
                "transaction_total": 100000,
                "transaction_status": "Belum Bayar",
                "deleted_at": null,
                "created_at": "2021-05-13T14:41:11.000000Z",
                "updated_at": "2021-05-13T14:41:11.000000Z"
            },
            "bukti_bayar": {
                "id": 1,
                "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
                "bukti_pembayaran": null,
                "deleted_at": null,
                "created_at": "2021-05-13T14:41:11.000000Z",
                "updated_at": "2021-05-13T14:41:11.000000Z"
            }
        }
    ]
}
```

- #### All Transaction Deleted (ADMIN)
    Request
    - Method: **GET**
    - Endpoint: **`/transaction/deleted`**
    - Header
      - Authorization: **`Bearer ${token}`**

    <br>
    Response
```json
{
    "status": "success",
    "data": [
        {
            "id": 1,
            "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
            "id_event": 2,
            "id_checkout_detail": 1,
            "id_bukti_bayar": 1,
            "created_by": null,
            "deleted_at": null,
            "created_at": "2021-05-13T14:41:11.000000Z",
            "updated_at": "2021-05-13T14:41:11.000000Z",
            "checkout_detail": {
                "id": 1,
                "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
                "name": "Imanuel Pay",
                "email": "imanuelpay@mail.com",
                "team_name": "SanSquad",
                "phone_number": "081234567890",
                "transaction_total": 100000,
                "transaction_status": "Belum Bayar",
                "deleted_at": null,
                "created_at": "2021-05-13T14:41:11.000000Z",
                "updated_at": "2021-05-13T14:41:11.000000Z"
            },
            "bukti_bayar": {
                "id": 1,
                "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
                "bukti_pembayaran": null,
                "deleted_at": null,
                "created_at": "2021-05-13T14:41:11.000000Z",
                "updated_at": "2021-05-13T14:41:11.000000Z"
            }
        }
    ]
}
```

- #### Show Transaction
    Request
    - Method: **GET**
    - Endpoint: **`/transaction/{uuid}`**

    <br>
    Response
```json
{
    "status": "success",
    "data": {
        "id": 1,
        "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
        "id_event": 2,
        "id_checkout_detail": 1,
        "id_bukti_bayar": 1,
        "created_by": null,
        "deleted_at": null,
        "created_at": "2021-05-13T14:41:11.000000Z",
        "updated_at": "2021-05-13T14:41:11.000000Z",
        "checkout_detail": {
            "id": 1,
            "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
            "name": "Imanuel Pay",
            "email": "imanuelpay@mail.com",
            "team_name": "SanSquad",
            "phone_number": "081234567890",
            "transaction_total": 100000,
            "transaction_status": "Belum Bayar",
            "deleted_at": null,
            "created_at": "2021-05-13T14:41:11.000000Z",
            "updated_at": "2021-05-13T14:41:11.000000Z"
        },
        "bukti_bayar": {
            "id": 1,
            "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
            "bukti_pembayaran": null,
            "deleted_at": null,
            "created_at": "2021-05-13T14:41:11.000000Z",
            "updated_at": "2021-05-13T14:41:11.000000Z"
        },
        "event": {
            "id": 2,
            "name": "PMPL ID S5",
            "genre": "Tencent Gamming",
            "organizer": "PUBG INDONESIA",
            "slot": 20,
            "image": "pmpl_id_s5_1620916703.png",
            "price_pool": 20000000,
            "fee": 100000,
            "description": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
            "detail": null,
            "address": null,
            "venue": "Kota Kupang",
            "status": "1",
            "date": "2021-05-20 00:00:00",
            "created_at": "2021-05-13T14:38:23.000000Z",
            "updated_at": "2021-05-13T14:38:23.000000Z"
        }
    }
}
```

- #### Transaction by User
    Request
    - Method: **GET**
    - Endpoint: **`/user/{created_by}/transaction`**

    <br>
    Response
```json
{
    "status": "success",
    "data": [
        {
            "id": 1,
            "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
            "id_event": 2,
            "id_checkout_detail": 1,
            "id_bukti_bayar": 1,
            "created_by": null,
            "deleted_at": null,
            "created_at": "2021-05-13T14:41:11.000000Z",
            "updated_at": "2021-05-13T14:41:11.000000Z",
            "checkout_detail": {
                "id": 1,
                "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
                "name": "Imanuel Pay",
                "email": "imanuelpay@mail.com",
                "team_name": "SanSquad",
                "phone_number": "081234567890",
                "transaction_total": 100000,
                "transaction_status": "Belum Bayar",
                "deleted_at": null,
                "created_at": "2021-05-13T14:41:11.000000Z",
                "updated_at": "2021-05-13T14:41:11.000000Z"
            },
            "bukti_bayar": {
                "id": 1,
                "uuid": "686bbd76-aeeb-4295-ac40-d97a63c5f0be",
                "bukti_pembayaran": null,
                "deleted_at": null,
                "created_at": "2021-05-13T14:41:11.000000Z",
                "updated_at": "2021-05-13T14:41:11.000000Z"
            }
        }
    ]
}
```

- #### Edit Transaction (ADMIN)
    Request
    - Method: **POST**
    - Endpoint: **`'/transaction/{uuid}`**
    - Header
      - Content-Type: application/json
      - Authorization: **`Bearer ${token}`**
    - Body
        Request | Rule
        -------- | ------
        transaction_status | nullable, string
        name | required, string
        email | required, email
        team_name | required, string
        phone_number | required, string

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully updated"
}
```

- #### Delete Transaction
    Request
    - Method: **DELETE**
    - Endpoint: **`/transaction/{uuid}`**

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully deleted"
}
```

- #### Force Delete Transaction (ADMIN)
    Request
    - Method: **DELETE**
    - Endpoint: **`/transaction/{uuid}/force-delete`**
    - Header
      - Authorization: **`Bearer ${token}`**

    <br>
    Response
```json
{
    "status": "success",
    "message": "successfully force deleted"
}
```
