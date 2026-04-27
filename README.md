FORMAT: 1A
HOST: https://app.yfsdelivery.com/api/

# YallaFelSekka

<strong>YFS Developer guide for API integration</strong>

## Base URL 
All URLs referenced in the documentation have the following base:


###   https://app.yfsdelivery.com/api/
   
Note: You need to change `Mock Server` to `Production` if you want to run it inside the documentation.

## Service Types

<table >
<tr><td style="padding-left: 0;" ><strong>Type</strong><td style="padding-left: 0;" ><strong>Value </strong></td><td style="padding-left: 0;" ><strong>Description </strong></td></tr>
<tr><td style="padding-left: 0;" >Delivery</td><td ><code>1</code></td><td>Standard Delivery.</td></tr>
<tr><td style="padding-left: 0;" >Exchange</td><td><code>2</code></td><td>Return + Replacement.</td></tr>
<tr><td style="padding-left: 0;" >CRP (Customer Return Pickup)</td><td><code>3</code></td><td>Return only.</td></tr>
</table>
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

<table >
<tr><td style="padding-left: 0;" ><strong>Status</strong><td style="padding-left: 0;" ><strong>Value </strong></td><td style="padding-left: 0;" ><strong>Description </strong></td></tr>
<tr><td style="padding-left: 0;" >Assigned</td><td ><code>0</code></td><td>The task has been assigned to a agent.</td></tr>
<tr><td style="padding-left: 0;" >Started</td><td><code>1</code></td><td>The task has been started and the agent is on the way.</td></tr>
<tr><td style="padding-left: 0;" >Successful</td><td><code>2</code></td><td>The task has been completed successfully.</td></tr>
<tr><td style="padding-left: 0;" >Failed</td><td><code>3</code></td><td>The task has been completed unsuccessfully.</td></tr>
<tr><td style="padding-left: 0;" >InProgress/Arrived</td><td><code>4</code></td><td>The task is being performed and the agent has reached the destination.</td></tr>
<tr><td style="padding-left: 0;" >Unassigned</td><td><code>6</code></td><td>The task has not been assigned to any agent.</td></tr>
<tr><td style="padding-left: 0;" >Accepted/Acknowledged</td><td><code>7</code></td><td>The task has been accepted by the agent which is assigned to him.</td></tr>
<tr><td style="padding-left: 0;" >Decline</td><td><code>8</code></td><td>The task has been declined by the agent which is assigned to him.</td></tr>
<tr><td style="padding-left: 0;" >Cancel</td><td><code>9</code></td><td>The task has been cancelled.</td></tr>
</table>

## E-Commerce Order Statuses

<table>
    <tr>
        <th>Status</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><strong>Task on Hold</strong></td>
        <td>Order/task is put on hold.</td>
    </tr> <!-- Unassigned / Pickup -->
    <tr>
        <td><strong>Unassigned</strong></td>
        <td>Delivery task is not assigned to any agent</td>
    </tr>
    <tr>
        <td><strong>Pickup Unassigned</strong></td>
        <td>Pickup task is not assigned to any agent.</td>
    </tr> <!-- Pickup -->
    <tr>
        <td><strong>Pickup Started</strong></td>
        <td>Pickup task has started.</td>
    </tr>
    <tr>
        <td><strong>Pickup Inprogress</strong></td>
        <td>Pickup is ongoing.</td>
    </tr>
    <tr>
        <td><strong>Pickup Assigned</strong></td>
        <td>Pickup task assigned to an agent.</td>
    </tr>
    <tr>
        <td><strong>Pickup Collected</strong></td>
        <td>Items collected from merchant.</td>
    </tr> <!-- Warehouse Received -->
    <tr>
        <td><strong>Received at Hub</strong></td>
        <td>Order received at a hub warehouse.</td>
    </tr>
    <tr>
        <td><strong>Received at Main Hub</strong></td>
        <td>Order received at the main warehouse.</td>
    </tr> <!-- Warehouse-to-Warehouse -->
    <tr>
        <td><strong>Manifest Created</strong></td>
        <td>Warehouse-to-warehouse manifest created.</td>
    </tr>
    <tr>
        <td><strong>In Transit to WH</strong></td>
        <td>Order in transit between warehouses.</td>
    </tr> <!-- Backward Transfer -->
    <tr>
        <td><strong>Backward Manifest Created</strong></td>
        <td>Reverse transfer manifest created.</td>
    </tr>
    <tr>
        <td><strong>Returning to Hub</strong></td>
        <td>Order is returning to hub warehouse.</td>
    </tr>
    <tr>
        <td><strong>Returning to Main WH</strong></td>
        <td>Order is returning to main warehouse.</td>
    </tr>
    <tr>
        <td><strong>Return Received in Hub</strong></td>
        <td>Reverse transfer received at hub.</td>
    </tr>
    <tr>
        <td><strong>Return Received in Main WH</strong></td>
        <td>Reverse transfer received at main warehouse.</td>
    </tr> <!-- Warehouse-to-Merchant (RTV) -->
    <tr>
        <td><strong>Returning to Merchant</strong></td>
        <td>Return-to-merchant initiated.</td>
    </tr>
    <tr>
        <td><strong>In Transit to Merchant</strong></td>
        <td>Order on the way back to merchant.</td>
    </tr> <!-- Delivery -->
    <tr>
        <td><strong>Out for Delivery</strong></td>
        <td>Order assigned and agent is heading for delivery.</td>
    </tr>
    <tr>
        <td><strong>Exchange Assigned</strong></td>
        <td>Exchange request assigned to an agent.</td>
    </tr>
    <tr>
        <td><strong>Delivery Attempt in Progress</strong></td>
        <td>Delivery attempt started but not completed.</td>
    </tr>
    <tr>
        <td><strong>Delivered Successfully</strong></td>
        <td>Order delivered.</td>
    </tr>
    <tr>
        <td><strong>Exchange Successful</strong></td>
        <td>Exchange order completed successfully.</td>
    </tr>
    <tr>
        <td><strong>Delivery Attempt Failed</strong></td>
        <td>Agent attempted but failed to deliver.</td>
    </tr> <!-- Cancel / Failed -->
    <tr>
        <td><strong>Pickup Cancelled</strong></td>
        <td>Pickup was cancelled.</td>
    </tr>
    <tr>
        <td><strong>Manifest Cancelled</strong></td>
        <td>Warehouse transfer manifest cancelled.</td>
    </tr>
    <tr>
        <td><strong>Cancelled</strong></td>
        <td>Order cancelled due to general reasons.</td>
    </tr> <!-- Special Cancel Case -->
    <tr>
        <td><strong>Returned to vendor</strong></td>
        <td>Cancelled with RTV reason.</td>
    </tr> <!-- Fallback -->
</table>

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


## Add New Order [/orders/addorder]

### /orders/addorder [POST]
<b>Note:</b> `/addorder` API is only for `delivery` and `exchange` orders.

<table >
<tr><td style="padding-left: 0;" ><strong>Field Name</strong><td style="padding-left: 0;" ><strong>Value </strong></td><td style="padding-left: 0;" ><strong>Required</strong></td><td style="padding-left: 0;" ><strong>Description </strong></td></tr>
<tr><td style="padding-left: 0;" >api_token</td><td ><code>Hashed Key From YFS</code></td><td>Required</td><td>Access token authorized to access the API library. Provided from YFS.</td></tr>
<tr><td style="padding-left: 0;" >service_type</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >orderid</td><td><code>String</code></td><td>Optional</td><td>Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system</td></tr>
<tr><td style="padding-left: 0;" >order_date</td><td><code>DateTime</code></td><td>Required</td><td>Date & Time of the order to be Delivered / Pickedup</td></tr>
<tr><td style="padding-left: 0;" >order_type</td><td><code>Integer</code></td><td>Required</td><td>Order type: Pickup = 0, Delivery = 1</td></tr>
<tr><td style="padding-left: 0;" >transport_type</td><td><code>Integer</code></td><td>Optional</td><td>Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van</td></tr>
<tr><td style="padding-left: 0;" >barcode</td><td><code>Text</code></td><td>Optional</td><td>Barcode for the order</td></tr>
<tr><td style="padding-left: 0;" >eng_name</td><td><code>Text</code></td><td>Required</td><td>Customer English full name</td></tr>
<tr><td style="padding-left: 0;" >ar_name</td><td><code>Text</code></td><td>Optional</td><td>Customer Arabic full name</td></tr>
<tr><td style="padding-left: 0;" >mobile</td><td><code>Text</code></td><td>Required</td><td>Customer Mobile number</td></tr>
<tr><td style="padding-left: 0;" >phone</td><td><code>Text</code></td><td>Optional</td><td>Customer Phone number</td></tr>
<tr><td style="padding-left: 0;" >email</td><td><code>Text (Email Format)</code></td><td>Optional</td><td> Customer Email address</td></tr>
<tr><td style="padding-left: 0;" >latitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Latitude)</td></tr>
<tr><td style="padding-left: 0;" >longitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Longitude)</td></tr>
<tr><td style="padding-left: 0;" >total_amount</td><td><code>Double (10,2)</code></td><td>Required</td><td>Amount to be collected from the customer.</td></tr>
<tr><td style="padding-left: 0;" >shipment_amount</td><td><code>Double (10,2)</code></td><td>Optional</td><td>Value of shipment.</td></tr>
<tr><td style="padding-left: 0;" >currency_code</td><td><code>String</code></td><td>Optional</td><td>Currency of amount to be collected. Default (EGP)</td></tr>
<tr><td style="padding-left: 0;" >require_refrigerator</td><td><code>Boolean</code></td><td>Optional</td><td>If the package requires special cooling conditions, Default 0</td></tr>
<tr><td style="padding-left: 0;" >number_of_parcels</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >building_no</td><td><code>Text</code></td><td>Optional</td><td>Building number for the customer</td></tr>
<tr><td style="padding-left: 0;" >street_address</td><td><code>Text</code></td><td>Required</td><td>Street address of the customer</td></tr>
<tr><td style="padding-left: 0;" >district</td><td><code>Text</code></td><td>Required</td><td>District of the customer</td></tr>
<tr><td style="padding-left: 0;" >landmark</td><td><code>Text</code></td><td>Optional</td><td>Any landmark near the customer address to help the agent reach the address easily.</td></tr>
<tr><td style="padding-left: 0;" >area</td><td><code>Text</code></td><td>Optional</td><td>Area of the customer address</td></tr>
<tr><td style="padding-left: 0;" >notes</td><td><code>Text</code></td><td>Optional</td><td>Special notes and remarks for the order</td></tr>
<tr><td style="padding-left: 0;" >agent_id</td><td><code>Integer</code></td><td>Optional</td><td>Agent (Captain) ID to assign the task to directly</td></tr>
<tr><td style="padding-left: 0;" >agent_mobile</td><td><code>Text</code></td><td>Optional</td><td>Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them</td></tr>
<tr><td style="padding-left: 0;" >shop_key</td><td><code>Text</code></td><td>Optional</td><td>Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order</td></tr>
<tr><td style="padding-left: 0;" >instant_delivery</td><td><code>Boolean</code></td><td>Optional</td><td>If the shipment requires instant delivery, Default false</td></tr>

</table>

+ Request (application/json)

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
        
+ Response 200 (application/json)

{
    "status": "success",
    "msg": "Order Created successfully",
    "id": "125407739"   //ID of the newly created order, this ID will be used for any Update/Cancel/Delete operations for the order
}
        
## Add Multiple Orders [/orders/addmultipleorders]

This API is used to create multiple pickup and delivery tasks at once.

### /orders/addmultipleorders [POST]

<table >
<tr><td style="padding-left: 0;" ><strong>Field Name</strong><td style="padding-left: 0;" ><strong>Value </strong></td><td style="padding-left: 0;" ><strong>Required</strong></td><td style="padding-left: 0;" ><strong>Description </strong></td></tr>
<tr><td style="padding-left: 0;" >api_token</td><td ><code>Hashed Key From YFS</code></td><td>Required</td><td>Access token authorized to access the API library. Provided from YFS.</td></tr>
<tr><td style="padding-left: 0;" >service_type</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >orderid</td><td><code>String</code></td><td>Optional</td><td>Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system</td></tr>
<tr><td style="padding-left: 0;" >order_date</td><td><code>DateTime</code></td><td>Required</td><td>Date & Time of the order to be Delivered / Pickedup</td></tr>
<tr><td style="padding-left: 0;" >order_type</td><td><code>Integer</code></td><td>Required</td><td>Order type: Pickup = 0, Delivery = 1</td></tr>
<tr><td style="padding-left: 0;" >transport_type</td><td><code>Integer</code></td><td>Optional</td><td>Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van</td></tr>
<tr><td style="padding-left: 0;" >barcode</td><td><code>Text</code></td><td>Optional</td><td>Barcode for the order</td></tr>
<tr><td style="padding-left: 0;" >eng_name</td><td><code>Text</code></td><td>Required</td><td>Customer English full name</td></tr>
<tr><td style="padding-left: 0;" >ar_name</td><td><code>Text</code></td><td>Optional</td><td>Customer Arabic full name</td></tr>
<tr><td style="padding-left: 0;" >mobile</td><td><code>Text</code></td><td>Required</td><td>Customer Mobile number</td></tr>
<tr><td style="padding-left: 0;" >phone</td><td><code>Text</code></td><td>Optional</td><td>Customer Phone number</td></tr>
<tr><td style="padding-left: 0;" >email</td><td><code>Text (Email Format)</code></td><td>Optional</td><td> Customer Email address</td></tr>
<tr><td style="padding-left: 0;" >latitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Latitude)</td></tr>
<tr><td style="padding-left: 0;" >longitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Longitude)</td></tr>
<tr><td style="padding-left: 0;" >total_amount</td><td><code>Double (10,2)</code></td><td>Required</td><td>Amount to be collected from the customer.</td></tr>
<tr><td style="padding-left: 0;" >shipment_amount</td><td><code>Double (10,2)</code></td><td>Optional</td><td>Value of shipment.</td></tr>
<tr><td style="padding-left: 0;" >currency_code</td><td><code>String</code></td><td>Optional</td><td>Currency of amount to be collected. Default (EGP)</td></tr>
<tr><td style="padding-left: 0;" >require_refrigerator</td><td><code>Boolean</code></td><td>Optional</td><td>If the package requires special cooling conditions, Default 0</td></tr>
<tr><td style="padding-left: 0;" >number_of_parcels</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >building_no</td><td><code>Text</code></td><td>Optional</td><td>Building number for the customer</td></tr>
<tr><td style="padding-left: 0;" >street_address</td><td><code>Text</code></td><td>Required</td><td>Street address of the customer</td></tr>
<tr><td style="padding-left: 0;" >district</td><td><code>Text</code></td><td>Required</td><td>District of the customer</td></tr>
<tr><td style="padding-left: 0;" >landmark</td><td><code>Text</code></td><td>Optional</td><td>Any landmark near the customer address to help the agent reach the address easily.</td></tr>
<tr><td style="padding-left: 0;" >area</td><td><code>Text</code></td><td>Optional</td><td>Area of the customer address</td></tr>
<tr><td style="padding-left: 0;" >notes</td><td><code>Text</code></td><td>Optional</td><td>Special notes and remarks for the order</td></tr>
<tr><td style="padding-left: 0;" >agent_id</td><td><code>Integer</code></td><td>Optional</td><td>Agent (Captain) ID to assign the task to directly</td></tr>
<tr><td style="padding-left: 0;" >agent_mobile</td><td><code>Text</code></td><td>Optional</td><td>Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them</td></tr>
<tr><td style="padding-left: 0;" >shop_key</td><td><code>Text</code></td><td>Optional</td><td>Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order</td></tr>
<tr><td style="padding-left: 0;" >instant_delivery</td><td><code>Boolean</code></td><td>Optional</td><td>If the shipment requires instant delivery, Default false</td></tr>

</table>

+ Request (application/json)

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
        
+ Response 200 (application/json)

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

## V2-Add Multiple Orders [/orders/v2/addmultipleorders]

This API is used to create multiple service_type orders at once.

### /orders/v2/addmultipleorders [POST]

<table >
<tr><td style="padding-left: 0;" ><strong>Field Name</strong><td style="padding-left: 0;" ><strong>Value </strong></td><td style="padding-left: 0;" ><strong>Required</strong></td><td style="padding-left: 0;" ><strong>Description </strong></td></tr>
<tr><td style="padding-left: 0;" >api_token</td><td ><code>Hashed Key From YFS</code></td><td>Required</td><td>Access token authorized to access the API library. Provided from YFS.</td></tr>
<tr><td style="padding-left: 0;" >service_type</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >orderid</td><td><code>String</code></td><td>Optional</td><td>Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system</td></tr>
<tr><td style="padding-left: 0;" >order_date</td><td><code>DateTime</code></td><td>Required</td><td>Date & Time of the order to be Delivered / Pickedup</td></tr>
<tr><td style="padding-left: 0;" >order_type</td><td><code>Integer</code></td><td>Required</td><td>Order type: Pickup = 0, Delivery = 1</td></tr>
<tr><td style="padding-left: 0;" >transport_type</td><td><code>Integer</code></td><td>Optional</td><td>Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van</td></tr>
<tr><td style="padding-left: 0;" >barcode</td><td><code>Text</code></td><td>Optional</td><td>Barcode for the order</td></tr>
<tr><td style="padding-left: 0;" >eng_name</td><td><code>Text</code></td><td>Required</td><td>Customer English full name</td></tr>
<tr><td style="padding-left: 0;" >ar_name</td><td><code>Text</code></td><td>Optional</td><td>Customer Arabic full name</td></tr>
<tr><td style="padding-left: 0;" >mobile</td><td><code>Text</code></td><td>Required</td><td>Customer Mobile number</td></tr>
<tr><td style="padding-left: 0;" >phone</td><td><code>Text</code></td><td>Optional</td><td>Customer Phone number</td></tr>
<tr><td style="padding-left: 0;" >email</td><td><code>Text (Email Format)</code></td><td>Optional</td><td> Customer Email address</td></tr>
<tr><td style="padding-left: 0;" >latitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Latitude)</td></tr>
<tr><td style="padding-left: 0;" >longitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Longitude)</td></tr>
<tr><td style="padding-left: 0;" >total_amount</td><td><code>Double (10,2)</code></td><td>Required</td><td>Amount to be collected from the customer.</td></tr>
<tr><td style="padding-left: 0;" >shipment_amount</td><td><code>Double (10,2)</code></td><td>Optional</td><td>Value of shipment.</td></tr>
<tr><td style="padding-left: 0;" >currency_code</td><td><code>String</code></td><td>Optional</td><td>Currency of amount to be collected. Default (EGP)</td></tr>
<tr><td style="padding-left: 0;" >require_refrigerator</td><td><code>Boolean</code></td><td>Optional</td><td>If the package requires special cooling conditions, Default 0</td></tr>
<tr><td style="padding-left: 0;" >number_of_parcels</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >building_no</td><td><code>Text</code></td><td>Optional</td><td>Building number for the customer</td></tr>
<tr><td style="padding-left: 0;" >street_address</td><td><code>Text</code></td><td>Required</td><td>Street address of the customer</td></tr>
<tr><td style="padding-left: 0;" >district</td><td><code>Text</code></td><td>Required</td><td>District of the customer</td></tr>
<tr><td style="padding-left: 0;" >landmark</td><td><code>Text</code></td><td>Optional</td><td>Any landmark near the customer address to help the agent reach the address easily.</td></tr>
<tr><td style="padding-left: 0;" >area</td><td><code>Text</code></td><td>Optional</td><td>Area of the customer address</td></tr>
<tr><td style="padding-left: 0;" >notes</td><td><code>Text</code></td><td>Optional</td><td>Special notes and remarks for the order</td></tr>
<tr><td style="padding-left: 0;" >agent_id</td><td><code>Integer</code></td><td>Optional</td><td>Agent (Captain) ID to assign the task to directly</td></tr>
<tr><td style="padding-left: 0;" >agent_mobile</td><td><code>Text</code></td><td>Optional</td><td>Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them</td></tr>
<tr><td style="padding-left: 0;" >shop_key</td><td><code>Text</code></td><td>Optional</td><td>Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order</td></tr>
<tr><td style="padding-left: 0;" >instant_delivery</td><td><code>Boolean</code></td><td>Optional</td><td>If the shipment requires instant delivery, Default false</td></tr>

</table>

+ Request (application/json)

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

        
+ Response 200 (application/json)

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

## Update Order [/orders/updateorder]

### /orders/updateorder [POST]

Update order details.<br/>
<b>Note:</b> Only delivery service_type orders are allowed to be updated.

<table >
<tr><td style="padding-left: 0;" ><strong>Field Name</strong><td style="padding-left: 0;" ><strong>Value </strong></td><td style="padding-left: 0;" ><strong>Required</strong></td><td style="padding-left: 0;" ><strong>Description </strong></td></tr>
<tr><td style="padding-left: 0;" >api_token</td><td ><code>Hashed Key From YFS</code></td><td>Required</td><td>Access token authorized to access the API library. Provided from YFS.</td></tr>
<tr><td style="padding-left: 0;" >id</td><td><code>BigInt</code></td><td>Required</td><td>The OrderID generated when the Order was first created.</td></tr>
<tr><td style="padding-left: 0;" >orderid</td><td><code>String</code></td><td>Optional</td><td>Order ID generated from the requesting system to YFS to keep track of orders created on YFS and their matching orders on the client system</td></tr>
<tr><td style="padding-left: 0;" >order_date</td><td><code>DateTime</code></td><td>Required</td><td>Date & Time of the order to be Delivered / Pickedup</td></tr>
<tr><td style="padding-left: 0;" >transport_type</td><td><code>Integer</code></td><td>Optional</td><td>Transport type required for the order: 1 = Car, 2 = Bike (Default), 6 = Truck, 8 = Van</td></tr>
<tr><td style="padding-left: 0;" >barcode</td><td><code>Text</code></td><td>Optional</td><td>Barcode for the order</td></tr>
<tr><td style="padding-left: 0;" >eng_name</td><td><code>Text</code></td><td>Required</td><td>Customer English full name</td></tr>
<tr><td style="padding-left: 0;" >ar_name</td><td><code>Text</code></td><td>Optional</td><td>Customer Arabic full name</td></tr>
<tr><td style="padding-left: 0;" >mobile</td><td><code>Text</code></td><td>Required</td><td>Customer Mobile number</td></tr>
<tr><td style="padding-left: 0;" >phone</td><td><code>Text</code></td><td>Optional</td><td>Customer Phone number</td></tr>
<tr><td style="padding-left: 0;" >email</td><td><code>Text (Email Format)</code></td><td>Optional</td><td> Customer Email address</td></tr>
<tr><td style="padding-left: 0;" >latitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Latitude)</td></tr>
<tr><td style="padding-left: 0;" >longitude</td><td><code>Text</code></td><td>Optional</td><td>Customer location coordinates (Longitude)</td></tr>
<tr><td style="padding-left: 0;" >total_amount</td><td><code>Double (10,2)</code></td><td>Required</td><td>Amount to be collected from the customer.</td></tr>
<tr><td style="padding-left: 0;" >shipment_amount</td><td><code>Double (10,2)</code></td><td>Optional</td><td>Value of shipment.</td></tr>
<tr><td style="padding-left: 0;" >currency_code</td><td><code>String</code></td><td>Optional</td><td>Currency of amount to be collected. Default (EGP)</td></tr>
<tr><td style="padding-left: 0;" >require_refrigerator</td><td><code>Boolean</code></td><td>Optional</td><td>If the package requires special cooling conditions, Default 0</td></tr>
<tr><td style="padding-left: 0;" >number_of_parcels</td><td><code>Integer</code></td><td>Optional</td><td>1 (Default)</td></tr>
<tr><td style="padding-left: 0;" >building_no</td><td><code>Text</code></td><td>Optional</td><td>Building number for the customer</td></tr>
<tr><td style="padding-left: 0;" >street_address</td><td><code>Text</code></td><td>Required</td><td>Street address of the customer</td></tr>
<tr><td style="padding-left: 0;" >district</td><td><code>Text</code></td><td>Required</td><td>District of the customer</td></tr>
<tr><td style="padding-left: 0;" >landmark</td><td><code>Text</code></td><td>Optional</td><td>Any landmark near the customer address to help the agent reach the address easily.</td></tr>
<tr><td style="padding-left: 0;" >area</td><td><code>Text</code></td><td>Optional</td><td>Area of the customer address</td></tr>
<tr><td style="padding-left: 0;" >notes</td><td><code>Text</code></td><td>Optional</td><td>Special notes and remarks for the order</td></tr>
<tr><td style="padding-left: 0;" >agent_id</td><td><code>Integer</code></td><td>Optional</td><td>Agent (Captain) ID to assign the task to directly</td></tr>
<tr><td style="padding-left: 0;" >agent_mobile</td><td><code>Text</code></td><td>Optional</td><td>Agent (Captain) Mobile Number, If no Agent Id sent then will use the phone number to search for the agent and assign the task to them</td></tr>
<tr><td style="padding-left: 0;" >shop_key</td><td><code>Text</code></td><td>Optional</td><td>Unique Shop Identifier from the customer side. If an account has more than one shop sending orders, then this key will be used to identify which shop created that order</td></tr>
<tr><td style="padding-left: 0;" >instant_delivery</td><td><code>Boolean</code></td><td>Optional</td><td>If the shipment requires instant delivery, Default false</td></tr>

</table>

+ Request (application/json)

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

+ Response 201 (application/json)

    + Body

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
            
## Cancel Order [/orders/cancelorder]

### /orders/cancelorder [POST]

Cancel an order using its job_id.

+ Request (application/json)

        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
            "id":125407739
        }

+ Response 201 (application/json)

    + Body

{
    "status": "success",
    "msg": "Order successfully cancelled"
}
            


## Get Order Details [/orders/orderdetails]

### /orders/orderdetails [POST]

Retrive the order details using the Order ID.

+ Request (application/json)

        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
            "id":125407739
        }

+ Response 201 (application/json)

    + Body

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
            
## Get Order Details By ID's [/orders/orderdetails_by_ids]

### /orders/orderdetails_by_ids [POST]

Retrive the orders details using the Order ID List.

+ Request (application/json)

        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
            "ids": [23454, 23455, 23456]
        }

+ Response 201 (application/json)

    + Body
{
    "status": "success",
    "data": {<Array of order details>}
}
            

## Get Orders History [/orders/orders_history_by_ids]

### /orders/orders_history_by_ids [POST]

Retrive the orders history using the a list of Order ID's.

+ Request (application/json)

        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",
            "ids": [30667, 26544]
        }

+ Response 201 (application/json)

    + Body
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
            
## List All Orders [/orders/list]

### /orders/list [POST]

Retrive a list of all orders for a specified company using the authentication key.

+ Request (application/json)

        {
            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404"
        }

+ Response 201 (application/json)

    + Body
{
    "status": "success",
    "data": {<Array of order details>}
}

<!--## Get Order Location [/orders/get_order_location]-->

<!--### /orders/get_order_location [POST]-->

<!--Retrive the Location coordinates of order(s) using either the Task ID or the sent Order ID.-->
<!--The filters can be either "id" or "orderid" or both fields.-->

+ Request (application/json)

<!--        {-->
<!--            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",-->
<!--            "id":[105984],-->
<!--            "orderid":["Pickup-888887686932", "Dropoff-8876627686932"],-->
<!--        }-->

+ Response 200 (application/json)

<!--    + Body-->

<!--            [-->
<!--            {-->
<!--                "status": "success",-->
<!--                "msg": "",-->
<!--                "data": [-->
<!--                    {-->
<!--                        "id": 233271,-->
<!--                        "orderid": "Dropoff-8532327686932",-->
<!--                        "agent_id": 105984,-->
<!--                        "order_date": "2021-11-11 16:24:08",-->
<!--                        "status": "Received",-->
<!--                        "mobile": "+201001466124",-->
<!--                        "order_type": "Delivery",-->
<!--                        "tracking_link": "https://app.yallafelsekka.com/tracking/index.html?jobID=f41d309c897e6f116c3bf141556d8a4d",-->
<!--                        "latitude": "29.9859544",-->
<!--                        "longitude": "30.9590604"-->
<!--                    },-->
<!--                    {-->
<!--                        "id": 233277,-->
<!--                        "orderid": "Pickup-888887686932",-->
<!--                        "agent_id": 1130081,-->
<!--                        "order_date": "2021-11-11 16:40:20",-->
<!--                        "status": "Received",-->
<!--                        "mobile": "+201018164888",-->
<!--                        "order_type": "Delivery",-->
<!--                        "tracking_link": "https://app.yallafelsekka.com/tracking/index.html?jobID=8a6cb0a6fc2e0e26b1b6c162cb447f27",-->
<!--                        "latitude": "30.0211754",-->
<!--                        "longitude": "31.4344284"-->
<!--                    },-->
<!--                    {-->
<!--                        "id": 233279,-->
<!--                        "orderid": "Dropoff-8876627686932",-->
<!--                        "agent_id": 1130381,-->
<!--                        "order_date": "2021-11-11 16:40:20",-->
<!--                        "status": "Received",-->
<!--                        "mobile": "+201018164888",-->
<!--                        "order_type": "Delivery",-->
<!--                        "tracking_link": "https://app.yallafelsekka.com/tracking/index.html?jobID=8a6cb0a6fc2e0e26b1b6c162cb447f27",-->
<!--                        "latitude": "30.0211754",-->
<!--                        "longitude": "31.4344284"-->
<!--                    }-->
<!--                ]-->
<!--            }-->
<!--            ]-->
            
<!--## Get Agent Location [/agents/agent_location]-->

<!--### /agents/agent_location [POST]-->

<!--Retrive the current Agent Location coordinates using the Agent ID.-->

+ Request (application/json)

<!--        {-->
<!--            "api_token":"fe7dce957a527e9c7b91f00bd697fade91a02bf0389544568b27950240478404",-->
<!--            "agent_id":105984-->
<!--        }-->

+ Response 200 (application/json)

<!--    + Body-->

<!--            [-->
<!--            {-->
<!--                "status": "success",-->
<!--                "data": [-->
<!--                    {-->
<!--                        "agent_id": 105984,-->
<!--                        "latitude":"30.0203254",-->
<!--                        "longitude":"31.492839"-->
<!--                    }-->
<!--                ]-->
<!--            }-->
<!--            ]-->
            

