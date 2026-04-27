# YallaFelSekka

**YFS Developer guide for API integration**

## Base URL

All URLs referenced in the documentation have the following base:

### https://app.yfsdelivery.com/api/

Note: You need to change `Mock Server` to `Production` if you want to run it inside the documentation.

## Service Types

| Type | Value | Description |
|------|-------|-------------|
| Delivery | `1` | Standard Delivery. |
| Exchange | `2` | Return + Replacement. |
| CRP (Customer Return Pickup) | `3` | Return only. |

###### Note:
If `service_type` is not provided, the default is **1 (Delivery)**.

### 🚚 Delivery
For `Delivery`, the client must create a delivery order using using `/addorder` or `addmultipleorders` API.

### 🔄 Exchange
For `Exchange`, the client must create a delivery order using using `/addorder` or `addmultipleorders` API.

### ↩️ CRP
For `CRP`, the client must create a pickup and delivery order using using `addmultipleorders` API.

#### CRP Example
```json
{
  "api_token": "256b83476ba7aa2ca0665015abc6bac286a4944d93b04c4f",
  "data": [
    {
      "service_type": 3,
      "orderid": "SYS0001",
      "order_date": "2020-11-15 14:00:00",
      "order_type": 0,  // Pickup Order
      "transport_type": 2,
      "barcode": "OR3FEZST",
      "eng_name": "Ahmed Hassan",
      "ar_name": "أحمد حسن",
      "mobile": "+201001434441",
      "phone": "0222551986",
      "email": "email@yfs.com",
      "latitude": "30.0203254",
      "longitude": "31.492839",
      "total_amount": 0,
      "shipment_amount": 100,
      "currency_code": "EGP",
      "require_refrigerator": 0,
      "number_of_parcels": 5,
      "building_no": "57",
      "street_address": "250, Degla",
      "district": "Degla",
      "landmark": "Behind Grand mall",
      "area": "Maadi",
      "notes": "Next to Alwaffa bank",
      "shop_key": "PX-172"
    },
    {
      "service_type": 3,
      "orderid": "SYS0001",
      "order_date": "2020-11-15 18:00:00",
      "order_type": 1, // Delivery Order
      "transport_type": 2,
      "barcode": "OR3TYIST",
      "eng_name": "Mohamed Ahmed",
      "ar_name": "محمد احمد",
      "mobile": "+201221434001",
      "phone": "0222551986",
      "email": "email@test.com",
      "latitude": "30.0203254",
      "longitude": "31.492839",
      "total_amount": 265.5,
      "shipment_amount": 300,
      "currency_code": "EGP",
      "require_refrigerator": 0,
      "number_of_parcels": 5,
      "building_no": "8",
      "street_address": "170, New Cairo",
      "district": "New Cairo",
      "landmark": "Mountain View Roundabout",
      "area": "New Cairo",
      "notes": "Near El Teseaan Street",
      "shop_key": "ZY-187"
    }
  ]
}
```

## Grocery Order Statuses

| Status | Value | Description |
|--------|-------|-------------|
| Assigned | `0` | The task has been assigned to a agent. |
| Started | `1` | The task has been started and the agent is on the way. |
| Successful | `2` | The task has been completed successfully. |
| Failed | `3` | The task has been completed unsuccessfully. |
| InProgress/Arrived | `4` | The task is being performed and the agent has reached the destination. |
| Unassigned | `6` | The task has not been assigned to any agent. |
| Accepted/Acknowledged | `7` | The task has been accepted by the agent which is assigned to him. |
| Decline | `8` | The task has been declined by the agent which is assigned to him. |
| Cancel | `9` | The task has been cancelled. |

## E-Commerce Order Statuses

| Status | Description |
|--------|-------------|
| **Task on Hold** | Order/task is put on hold. |
| **Unassigned** | Delivery task is not assigned to any agent |
| **Pickup Unassigned** | Pickup task is not assigned to any agent. |
| **Pickup Started** | Pickup task has started. |
| **Pickup Inprogress** | Pickup is ongoing. |
| **Pickup Assigned** | Pickup task assigned to an agent. |
| **Pickup Collected** | Items collected from merchant. |
| **Received at Hub** | Order received at a hub warehouse. |
| **Received at Main Hub** | Order received at the main warehouse. |
| **Manifest Created** | Warehouse-to-warehouse manifest created. |
| **In Transit to WH** | Order in transit between warehouses. |
| **Backward Manifest Created** | Reverse transfer manifest created. |
| **Returning to Hub** | Order is returning to hub warehouse. |
| **Returning to Main WH** | Order is returning to main warehouse. |
| **Return Received in Hub** | Reverse transfer received at hub. |
| **Return Received in Main WH** | Reverse transfer received at main warehouse. |
| **Returning to Merchant** | Return-to-merchant initiated. |
| **In Transit to Merchant** | Order on the way back to merchant. |
| **Out for Delivery** | Order assigned and agent is heading for delivery. |
| **Exchange Assigned** | Exchange request assigned to an agent. |
| **Delivery Attempt in Progress** | Delivery attempt started but not completed. |
| **Delivered Successfully** | Order delivered. |
| **Exchange Successful** | Exchange order completed successfully. |
| **Delivery Attempt Failed** | Agent attempted but failed to deliver. |
| **Pickup Cancelled** | Pickup was cancelled. |
| **Manifest Cancelled** | Warehouse transfer manifest cancelled. |
| **Cancelled** | Order cancelled due to general reasons. |
| **Returned to vendor** | Cancelled with RTV reason. |

## Cancel Reasons

| Code | Description |
|------|-------------|
| CC034 | Order is ready to be returned to the vendor |
| CC06 | Client asked to reschedule the package |
| CC016 | Customer wants to receive all of his/her orders |
| CC04 | Client phone is closed |
| CC02 | Client wrong number |
| CC09 | DA had an accident or a break down |
| CC032 | Customer rejected the order after opening it |
| CC10 | Out of zone |
| CC05 | Client rejected the package |
| CC031 | Order not received |
| CC027 | Reverse Collected |
| CC018 | Agent Fraud order stolen package / order lost |
| CC01 | Client not answering the phone |
| CC013 | Customer asked to change the location of receiving the package to another address |
| CC020 | Lost / damaged |
| CC026 | Updated Successful by Mistake |
| CC014 | Out of the courier zone |
| CC11 | Vendor asked to return the order |
| CC033 | Order reattempt |
| CC07 | Third attempt in 5 working days |
| CC03 | Client wrong address |
| CC017 | Customer wants to receive his/her order in Hub |
| CC019 | Order lost from Operations |
| CC030 | DA has denied the order |
| F003 | DA reached the customer and then customer rejected the package |
| CC08 | Package returned to vendor |
| CC012 | DA reached the customer and no one was there to receive the package |
| CC015 | Customer phone is out of service |
| CC40 | Missing Documents |

---

## Add New Order [/orders/addorder]

### /orders/addorder [POST]

<b>Note:</b> `/addorder` API is only for `delivery` and `exchange` orders.

| Field Name | Value | Required | Description |
|------------|-------|----------|-------------|
| api_token | `Hashed Key From YFS` | Required | Access token authorized to access the API library. Provided from YFS. |
| service_type | `Integer` | Optional | 1 (Default) |
| orderid | `String` | Optional | Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system |
| order_date | `DateTime` | Required | Date & Time of the order to be Delivered / Pickedup |
| order_type | `Integer` | Required | Order type: Pickup = 0, Delivery = 1 |
| transport_type | `Integer` | Optional | Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van |
| barcode | `Text` | Optional | Barcode for the order |
| eng_name | `Text` | Required | Customer English full name |
| ar_name | `Text` | Optional | Customer Arabic full name |
| mobile | `Text` | Required | Customer Mobile number |
| phone | `Text` | Optional | Customer Phone number |
| email | `Text (Email Format)` | Optional |  Customer Email address |
| latitude | `Text` | Optional | Customer location coordinates (Latitude) |
| longitude | `Text` | Optional | Customer location coordinates (Longitude) |
| total_amount | `Double (10,2)` | Required | Amount to be collected from the customer. |
| shipment_amount | `Double (10,2)` | Optional | Value of shipment. |
| currency_code | `String` | Optional | Currency of amount to be collected. Default (EGP) |
| require_refrigerator | `Boolean` | Optional | If the package requires special cooling conditions, Default 0 |
| number_of_parcels | `Integer` | Optional | 1 (Default) |
| building_no | `Text` | Optional | Building number for the customer |
| street_address | `Text` | Required | Street address of the customer |
| district | `Text` | Required | District of the customer |
| landmark | `Text` | Optional | Any landmark near the customer address to help the agent reach the address easily. |
| area | `Text` | Optional | Area of the customer address |
| notes | `Text` | Optional | Special notes and remarks for the order |
| agent_id | `Integer` | Optional | Agent (Captain) ID to assign the task to directly |
| agent_mobile | `Text` | Optional | Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them |
| shop_key | `Text` | Optional | Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order |
| instant_delivery | `Boolean` | Optional | If the shipment requires instant delivery, Default false |

**Request (application/json)**

```json
{
    "api_token": "256b83476ba7aa2ca0665015abc6bac286a4944d93b04c4f7967d91c953560a6",
    "service_type": 1,
    "orderid":"SYS0001",
    "order_date":"2020-11-15 14:00:00",
    "order_type": 1,
    "transport_type": 2,
    "barcode": "OR3FEZST",
    "eng_name":"Ahmed Hassan",
    "ar_name":"أحمد حسن",
    "mobile":"+201001434441",
    "phone":"0222551986",
    "email":"email@yfs.com",
    "latitude":"30.0203254",
    "longitude":"31.492839",
    "total_amount": 265.5,
    "shipment_amount": 300,
    "currency_code":"EGP",
    "require_refrigerator": 0,
    "number_of_parcels": 5,
    "building_no":"57",
    "street_address":"250, Degla",
    "district":"Degla",
    "landmark":"Behind Grand mall",
    "area":"Maadi",
    "notes":"Next to Alwaffa bank",
    "shop_key":"PX-172",
    "instant_delivery": false
}
```

**Response 200 (application/json)**

```json
{
    "status": "success",
    "msg": "Order Created successfully",
    "id": "125407739"   //ID of the newly created order, this ID will be used for any Update/Cancel/Delete operations for the order
}
```

---

## Add Multiple Orders [/orders/addmultipleorders]

This API is used to create multiple pickup and delivery tasks at once.

### /orders/addmultipleorders [POST]

| Field Name | Value | Required | Description |
|------------|-------|----------|-------------|
| api_token | `Hashed Key From YFS` | Required | Access token authorized to access the API library. Provided from YFS. |
| service_type | `Integer` | Optional | 1 (Default) |
| orderid | `String` | Optional | Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system |
| order_date | `DateTime` | Required | Date & Time of the order to be Delivered / Pickedup |
| order_type | `Integer` | Required | Order type: Pickup = 0, Delivery = 1 |
| transport_type | `Integer` | Optional | Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van |
| barcode | `Text` | Optional | Barcode for the order |
| eng_name | `Text` | Required | Customer English full name |
| ar_name | `Text` | Optional | Customer Arabic full name |
| mobile | `Text` | Required | Customer Mobile number |
| phone | `Text` | Optional | Customer Phone number |
| email | `Text (Email Format)` | Optional |  Customer Email address |
| latitude | `Text` | Optional | Customer location coordinates (Latitude) |
| longitude | `Text` | Optional | Customer location coordinates (Longitude) |
| total_amount | `Double (10,2)` | Required | Amount to be collected from the customer. |
| shipment_amount | `Double (10,2)` | Optional | Value of shipment. |
| currency_code | `String` | Optional | Currency of amount to be collected. Default (EGP) |
| require_refrigerator | `Boolean` | Optional | If the package requires special cooling conditions, Default 0 |
| number_of_parcels | `Integer` | Optional | 1 (Default) |
| building_no | `Text` | Optional | Building number for the customer |
| street_address | `Text` | Required | Street address of the customer |
| district | `Text` | Required | District of the customer |
| landmark | `Text` | Optional | Any landmark near the customer address to help the agent reach the address easily. |
| area | `Text` | Optional | Area of the customer address |
| notes | `Text` | Optional | Special notes and remarks for the order |
| agent_id | `Integer` | Optional | Agent (Captain) ID to assign the task to directly |
| agent_mobile | `Text` | Optional | Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them |
| shop_key | `Text` | Optional | Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order |
| instant_delivery | `Boolean` | Optional | If the shipment requires instant delivery, Default false |

**Request (application/json)**

```json
{
    "api_token": "256b83476ba7aa2ca0665015abc6bac286a4944d93b04c4f7967d91c953560a6",
    "data": [
                {
                    "service_type": 1,
                    "orderid":"SYS0001",
                    "order_date":"2020-11-15 14:00:00",
                    "order_type": 1,
                    "transport_type": 2,
                    "barcode": "OR3FEZST1",
                    "eng_name":"Ahmed Hassan",
                    "ar_name":"أحمد حسن",
                    "mobile":"+201001434441",
                    "phone":"0222551986",
                    "email":"email@yfs.com",
                    "latitude":"30.0203254",
                    "longitude":"31.492839",
                    "total_amount": 0,
                    "shipment_amount": 100,
                    "currency_code":"EGP",
                    "require_refrigerator": 0,
                    "number_of_parcels": 5,
                    "building_no":"57",
                    "street_address":"250, Degla",
                    "district":"Degla",
                    "landmark":"Behind Grand mall",
                    "area":"Maadi",
                    "notes":"Next to Alwaffa bank",
                    "shop_key":"PX-172",
                    "instant_delivery": false
                },
                {
                    "service_type": 1,
                    "orderid":"SYS0002",
                    "order_date":"2020-11-15 18:00:00",
                    "order_type": 1,
                    "transport_type": 2,
                    "barcode": "OR3FEZST2",
                    "eng_name":"Mohamed Ahmed",
                    "ar_name":"محمد احمد",
                    "mobile":"+201221434001",
                    "phone":"0222551986",
                    "email":"email@test.com",
                    "latitude":"30.0203254",
                    "longitude":"31.492839",
                    "total_amount": 265.5,
                    "shipment_amount": 300,
                    "currency_code":"EGP",
                    "require_refrigerator": 0,
                    "number_of_parcels": 5,
                    "building_no":"8",
                    "street_address":"170, New Cairo",
                    "district":"New Cairo",
                    "landmark":"Mountain View Roundabout",
                    "area":"New Cairo",
                    "notes":"Near El Teseaan Street",
                    "shop_key":"ZY-187",
                    "instant_delivery": false
                }
            ]
}
```

**Response 200 (application/json)**

```json
{
    "status": "success",
    "msg": "Order Created successfully.",
    "id": [
        [
            "PMKN-SYS0001",
            650967,
            2508287567828,
            "OR3FEZST1"
        ],
        [
            "PMKN-SYS0002",
            650968,
            250828581600,
            "OR3FEZST2"
        ]
    ]
}
```

---

## V2-Add Multiple Orders [/orders/v2/addmultipleorders]

This API is used to create multiple service_type orders at once.

### /orders/v2/addmultipleorders [POST]

| Field Name | Value | Required | Description |
|------------|-------|----------|-------------|
| api_token | `Hashed Key From YFS` | Required | Access token authorized to access the API library. Provided from YFS. |
| service_type | `Integer` | Optional | 1 (Default) |
| orderid | `String` | Optional | Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system |
| order_date | `DateTime` | Required | Date & Time of the order to be Delivered / Pickedup |
| order_type | `Integer` | Required | Order type: Pickup = 0, Delivery = 1 |
| transport_type | `Integer` | Optional | Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van |
| barcode | `Text` | Optional | Barcode for the order |
| eng_name | `Text` | Required | Customer English full name |
| ar_name | `Text` | Optional | Customer Arabic full name |
| mobile | `Text` | Required | Customer Mobile number |
| phone | `Text` | Optional | Customer Phone number |
| email | `Text (Email Format)` | Optional |  Customer Email address |
| latitude | `Text` | Optional | Customer location coordinates (Latitude) |
| longitude | `Text` | Optional | Customer location coordinates (Longitude) |
| total_amount | `Double (10,2)` | Required | Amount to be collected from the customer. |
| shipment_amount | `Double (10,2)` | Optional | Value of shipment. |
| currency_code | `String` | Optional | Currency of amount to be collected. Default (EGP) |
| require_refrigerator | `Boolean` | Optional | If the package requires special cooling conditions, Default 0 |
| number_of_parcels | `Integer` | Optional | 1 (Default) |
| building_no | `Text` | Optional | Building number for the customer |
| street_address | `Text` | Required | Street address of the customer |
| district | `Text` | Required | District of the customer |
| landmark | `Text` | Optional | Any landmark near the customer address to help the agent reach the address easily. |
| area | `Text` | Optional | Area of the customer address |
| notes | `Text` | Optional | Special notes and remarks for the order |
| agent_id | `Integer` | Optional | Agent (Captain) ID to assign the task to directly |
| agent_mobile | `Text` | Optional | Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them |
| shop_key | `Text` | Optional | Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order |
| instant_delivery | `Boolean` | Optional | If the shipment requires instant delivery, Default false |

**Request (application/json)**

```json
{
  "api_token": "256b83476ba7aa2ca0665015abc6bac286a4944d93b04c4f7967d91c953560a6",
  "orders": [
    {
      "service_type": 1,
      "data": {
        "orderid": "SYS0011",
        "order_date": "2026-04-27 18:00:00",
        "order_type": 1,
        "transport_type": 2,
        "barcode": "OR3FEZS11",
        "eng_name": "Mohamed Ahmed",
        "ar_name": "محمد احمد",
        "mobile": "+201221434001",
        "phone": "0222551986",
        "email": "email@test.com",
        "latitude": "30.0203254",
        "longitude": "31.492839",
        "total_amount": 265.5,
        "shipment_amount": 300,
        "currency_code": "EGP",
        "require_refrigerator": 0,
        "number_of_parcels": 5,
        "building_no": "8",
        "street_address": "170, New Cairo",
        "district": "New Cairo",
        "landmark": "Mountain View Roundabout",
        "area": "New Cairo",
        "notes": "Near El Teseaan Street",
        "shop_key": "ZY-187",
        "instant_delivery": false
      }
    },
    {
      "service_type": 2,
      "data": {
        "orderid": "SYS0021",
        "order_date": "2026-04-27 18:00:00",
        "order_type": 1,
        "transport_type": 2,
        "barcode": "OR3FEZS22",
        "eng_name": "Mohamed Ahmed",
        "ar_name": "محمد احمد",
        "mobile": "+201221434001",
        "phone": "0222551986",
        "email": "email@test.com",
        "latitude": "30.0203254",
        "longitude": "31.492839",
        "total_amount": 265.5,
        "shipment_amount": 300,
        "currency_code": "EGP",
        "require_refrigerator": 0,
        "number_of_parcels": 5,
        "building_no": "8",
        "street_address": "170, New Cairo",
        "district": "New Cairo",
        "landmark": "Mountain View Roundabout",
        "area": "New Cairo",
        "notes": "Near El Teseaan Street",
        "shop_key": "ZY-187",
        "instant_delivery": false
      }
    },
    {
      "service_type": 3,
      "data": [
        {
          "orderid": "SYS0033",
          "order_date": "2026-04-27 14:00:00",
          "order_type": 0,
          "transport_type": 2,
          "barcode": "OR3FEZS33",
          "eng_name": "Ahmed Hassan",
          "ar_name": "أحمد حسن",
          "mobile": "+201001434441",
          "phone": "0222551986",
          "email": "email@yfs.com",
          "latitude": "30.0203254",
          "longitude": "31.492839",
          "total_amount": 0,
          "shipment_amount": 0,
          "currency_code": "EGP",
          "require_refrigerator": 0,
          "number_of_parcels": 5,
          "building_no": "57",
          "street_address": "250, Degla",
          "district": "Degla",
          "landmark": "Behind Grand mall",
          "area": "Maadi",
          "notes": "Next to Alwaffa bank",
          "shop_key": "PX-172",
          "instant_delivery": false
        },
        {
          "orderid": "SYS0033",
          "order_date": "2026-04-27 18:00:00",
          "order_type": 1,
          "transport_type": 2,
          "barcode": "OR3FEZS33",
          "eng_name": "Mohamed Ahmed",
          "ar_name": "محمد احمد",
          "mobile": "+201221434001",
          "phone": "0222551986",
          "email": "email@test.com",
          "latitude": "30.0203254",
          "longitude": "31.492839",
          "total_amount": 0,
          "shipment_amount": 0,
          "currency_code": "EGP",
          "require_refrigerator": 0,
          "number_of_parcels": 5,
          "building_no": "8",
          "street_address": "170, New Cairo",
          "district": "New Cairo",
          "landmark": "Mountain View Roundabout",
          "area": "New Cairo",
          "notes": "Near El Teseaan Street",
          "shop_key": "ZY-187",
          "instant_delivery": false
        }
      ]
    }
  ]
}
```

**Response 200 (application/json)**

```json
{
    "status": "success",
    "msg": "Order Created successfully.",
    "orders": [
        {
            "order_id": "PMKN-SYS0011",
            "id": 662174,
            "job_id": 2604271267948,
            "barcode": "OR3FEZS11"
        },
        {
            "order_id": "PMKN-SYS0021",
            "id": 662175,
            "job_id": 2604271470393,
            "barcode": "OR3FEZS22"
        },
        {
            "order_id": "PMKN-SYS0033",
            "id": 662176,
            "job_id": 2604272482221,
            "barcode": "OR3FEZS33"
        },
        {
            "order_id": "PMKN-SYS0033",
            "id": 662177,
            "job_id": 2604278563523,
            "barcode": "OR3FEZS33"
        }
    ]
}
```

---

## Update Order [/orders/updateorder]

### /orders/updateorder [POST]

Update order details.<br/>
<b>Note:</b> Only delivery service_type orders are allowed to be updated.

| Field Name | Value | Required | Description |
|------------|-------|----------|-------------|
| api_token | `Hashed Key From YFS` | Required | Access token authorized to access the API library. Provided from YFS. |
| id | `BigInt` | Required | The OrderID generated when the Order was first created. |
| orderid | `String` | Optional | Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system |
| order_date | `DateTime` | Required | Date & Time of the order to be Delivered / Pickedup |
| transport_type | `Integer` | Optional | Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van |
| barcode | `Text` | Optional | Barcode for the order |
| eng_name | `Text` | Required | Customer English full name |
| ar_name | `Text` | Optional | Customer Arabic full name |
| mobile | `Text` | Required | Customer Mobile number |
| phone | `Text` | Optional | Customer Phone number |
| email | `Text (Email Format)` | Optional |  Customer Email address |
| latitude | `Text` | Optional | Customer location coordinates (Latitude) |
| longitude | `Text` | Optional | Customer location coordinates (Longitude) |
| total_amount | `Double (10,2)` | Required | Amount to be collected from the customer. |
| shipment_amount | `Double (10,2)` | Optional | Value of shipment. |
| currency_code | `String` | Optional | Currency of amount to be collected. Default (EGP) |
| require_refrigerator | `Boolean` | Optional | If the package requires special cooling conditions, Default 0 |
| number_of_parcels | `Integer` | Optional | 1 (Default) |
| building_no | `Text` | Optional | Building number for the customer |
| street_address | `Text` | Required | Street address of the customer |
| district | `Text` | Required | District of the customer |
| landmark | `Text` | Optional | Any landmark near the customer address to help the agent reach the address easily. |
| area | `Text` | Optional | Area of the customer address |
| notes | `Text` | Optional | Special notes and remarks for the order |
| agent_id | `Integer` | Optional | Agent (Captain) ID to assign the task to directly |
| agent_mobile | `Text` | Optional | Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them |
| shop_key | `Text` | Optional | Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order |
| instant_delivery | `Boolean` | Optional | If the shipment requires instant delivery, Default false |

**Request (application/json)**

```json
{
    "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
    "id":125407739,
    "orderid":"SYS0001",
    "order_date":"2020-11-15 14:00:00",
    "transport_type": 2,
    "barcode": "OR3FEZST",
    "eng_name":"Ahmed Hassan",
    "ar_name":"أحمد حسن",
    "mobile":"+201001434441",
    "phone":"0222551986",
    "email":"email@yfs.com",
    "latitude":"30.0203254",
    "longitude":"31.492839",
    "total_amount": 265.5,
    "shipment_amount": 300,
    "currency_code":"EGP",
    "require_refrigerator": 0,
    "number_of_parcels": 5,
    "building_no":"57",
    "street_address":"250, Degla",
    "district":"Degla",
    "landmark":"Behind Grand mall",
    "area":"Maadi",
    "notes":"Next to Alwaffa bank",
    "agent_id":48253,
    "agent_mobile": "+201001585897",
    "shop_key":"ZY-187",
    "instant_delivery": true
}
```

**Response 201 (application/json)**

```json
{
    "status": "success",
    "msg": "Order Updated successfully.",
    "data": [
        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
            "id":125407739,
            "orderid":"SYS0001",
            "order_date":"2020-11-15 14:00:00",
            "order_type": 1,
            "transport_type": 2,
            "barcode": "OR3FEZST",
            "eng_name":"Ahmed Hassan",
            "ar_name":"أحمد حسن",
            "mobile":"+201001434441",
            "phone":"0222551986",
            "email":"email@yfs.com",
            "latitude":"30.0203254",
            "longitude":"31.492839",
            "total_amount": 265.5,
            "currency_code":"EGP",
            "require_refrigerator": 0,
            "number_of_parcels": 5,
            "building_no":"57",
            "street_address":"250, Degla",
            "district":"Degla",
            "landmark":"Behind Grand mall",
            "area":"Maadi",
            "notes":"Next to Alwaffa bank",
            "agent_id":48253,
            "agent_mobile": "+201001585897",
            "shop_key":"ZY-187"
        }
    ]
}
```

---

## Cancel Order [/orders/cancelorder]

### /orders/cancelorder [POST]

Cancel an order using its job_id.

**Request (application/json)**

```json
{
    "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
    "id":125407739
}
```

**Response 201 (application/json)**

```json
{
    "status": "success",
    "msg": "Order successfully cancelled"
}
```

---

## Get Order Details [/orders/orderdetails]

### /orders/orderdetails [POST]

Retrive the order details using the Order ID.

**Request (application/json)**

```json
{
    "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
    "id":125407739
}
```

**Response 201 (application/json)**

```json
{
    "status": "success",
    "data": [
        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
            "id":125407739,
            "orderid":"SYS0001",
            "order_date":"2020-11-15 14:00:00",
            "order_type": 1,
            "transport_type": 2,
            "barcode": "OR3FEZST",
            "eng_name":"Ahmed Hassan",
            "ar_name":"أحمد حسن",
            "mobile":"+201001434441",
            "phone":"0222551986",
            "email":"email@yfs.com",
            "latitude":"30.0203254",
            "longitude":"31.492839",
            "total_amount": 265.5,
            "currency_code":"EGP",
            "require_refrigerator": 0,
            "number_of_parcels": 5,
            "building_no":"57",
            "street_address":"250, Degla",
            "district":"Degla",
            "landmark":"Behind Grand mall",
            "area":"Maadi",
            "notes":"Next to Alwaffa bank",
            "agent_id":48253,
            "agent_mobile": "+201001585897",
            "shop_key":"ZY-187",
            "tracking_link": "https://tracking.yallafelsekka.com/0cSGca166"
        }
    ]
}
```

---

## Get Order Details By ID's [/orders/orderdetails_by_ids]

### /orders/orderdetails_by_ids [POST]

Retrive the orders details using the Order ID List.

**Request (application/json)**

```json
{
    "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
    "ids": [23454, 23455, 23456]
}
```

**Response 201 (application/json)**

```json
{
    "status": "success",
    "data": {<Array of order details>}
}
```

---

## Get Orders History [/orders/orders_history_by_ids]

### /orders/orders_history_by_ids [POST]

Retrive the orders history using the a list of Order ID's.

**Request (application/json)**

```json
{
    "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
    "ids": [30667, 26544]
}
```

**Response 201 (application/json)**

```json
{
    "status": "success",
    "data": [
        {
            "30667": [
                        {
                            "id": 30667,
                            "orderid": "335275739",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "Assigned",
                            "latitude": null,
                            "longitude": null,
                            "creation_datetime": "2021-12-18 13:15:58"
                        },
                        {
                            "id": 30667,
                            "orderid": "335275739",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "Started",
                            "latitude": "31.2285228",
                            "longitude": "29.9618979",
                            "creation_datetime": "2021-12-19 00:55:12"
                        },
                        {
                            "id": 30667,
                            "orderid": "335275739",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "InProgress",
                            "latitude": "31.2285228",
                            "longitude": "29.9618979",
                            "creation_datetime": "2021-12-19 00:55:12"
                        },
                        {
                            "id": 30667,
                            "orderid": "335275739",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "Successful",
                            "latitude": "31.2285228",
                            "longitude": "29.9618979",
                            "creation_datetime": "2021-12-19 00:55:12"
                        }
                    ],
            "26544": [
                        {
                            "id": 26544,
                            "orderid": "8976465498",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "Assigned",
                            "latitude": null,
                            "longitude": null,
                            "creation_datetime": "2021-12-18 13:15:58"
                        },
                        {
                            "id": 26544,
                            "orderid": "8976465498",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "Started",
                            "latitude": "31.2285228",
                            "longitude": "29.9618979",
                            "creation_datetime": "2021-12-19 00:55:12"
                        },
                        {
                            "id": 26544,
                            "orderid": "8976465498",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "InProgress",
                            "latitude": "31.2285228",
                            "longitude": "29.9618979",
                            "creation_datetime": "2021-12-19 00:55:12"
                        },
                        {
                            "id": 26544,
                            "orderid": "8976465498",
                            "order_date": "2021-12-18 12:48:25",
                            "history_type": "Successful",
                            "latitude": "31.2285228",
                            "longitude": "29.9618979",
                            "creation_datetime": "2021-12-19 00:55:12"
                        }
                    ]
        }
    ]
}
```

---

## List All Orders [/orders/list]

### /orders/list [POST]

Retrive a list of all orders for a specified company using the authentication key.

**Request (application/json)**

```json
{
    "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404"
}
```

**Response 201 (application/json)**

```json
{
    "status": "success",
    "data": {<Array of order details>}
}
```
