### ORDER_RECEIVED
Order received on the OMS and waiting for processing.
```json
{
    "eventId": 1201895966044343901,
    "eventName": "order.received",
    "eventTimestamp": "2023-01-10T18:30:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeSlot": {
        "id": "slot1",
        "fromDate": "2023-01-11T14:00:00+00:00",
        "toDate": "2023-01-11T15:00:00+00:00"
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_CONFIRMED
Order confirmed by the OMS, waiting for shopper assignment.
```json
{
    "eventId": 1201895966044343902,
    "eventName": "order.confirmed",
    "eventTimestamp": "2023-01-10T18:31:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeSlot": {
        "id": "slot1",
        "fromDate": "2023-01-11T14:00:00+00:00",
        "toDate": "2023-01-11T15:00:00+00:00"
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_ALLOCATED
Order assigned and accepted by a shopper. In some cases, the order may be assigned to multiple resources (picker, courier).
```json
{
    "eventId": 1201895966044343903,
    "eventName": "order.allocated",
    "eventTimestamp": "2023-01-11T12:50:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeslot": {
        "id": "slot1",
        "fromDate": "2023-01-11T14:00:00+00:00",
        "toDate": "2023-01-11T15:00:00+00:00"
    },
    "shopper": {
        "id": "shopper-01",
        "name": "Lukasz",
        "avatarUrl": "https:\/\/media.lolamarket.com\/shopper\/lsdfdsf-sfdfs123-asd2.jpg"
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_RESCHEDULED
Order has been moved to a different timeslot, needs to be allocated.
```json
{
    "eventId": 1201895966044343904,
    "eventName": "order.rescheduled",
    "eventTimestamp": "2023-01-11T13:50:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "newTimeslot": {
        "id": "slot45",
        "fromDate": "2023-01-12T10:00:00+00:00",
        "toDate": "2023-01-12T11:00:00+00:00"
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_IN_PICKING
Shopper started picking items. Each product in the order will have their own status.
```json
{
    "eventId": 1201895966044343905,
    "eventName": "order.in.picking",
    "eventTimestamp": "2023-01-12T09:10:20Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeslot": {
        "id": "slot45",
        "fromDate": "2023-01-12T10:00:00+00:00",
        "toDate": "2023-01-12T11:00:00+00:00"
    },
    "shopper": {
        "id": "shopper-01",
        "name": "Lukasz",
        "avatarUrl": "https:\/\/media.lolamarket.com\/shopper\/lsdfdsf-sfdfs123-asd2.jpg"
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_PICKED
Shopper finished picking order items and will go to the cashier.
```json
{
    "eventId": 1201895966044343906,
    "eventName": "order.picked",
    "eventTimestamp": "2023-01-12T10:12:31Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeslot": {
        "id": "slot45",
        "fromDate": "2023-01-12T10:00:00+00:00",
        "toDate": "2023-01-12T11:00:00+00:00"
    },
    "shopper": {
        "id": "shopper-01",
        "name": "Lukasz",
        "avatarUrl": "https:\/\/media.lolamarket.com\/shopper\/lsdfdsf-sfdfs123-asd2.jpg"
    },
    "serviceType": "DELIVERY",
    "express": false,
    "articles": [
        {
        "itemId": "12345",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
        },
        {
        "itemId": "12346",
        "scanCode": "00980349941",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": true,
        "replacement": {
            "itemId": "12345"
        }
        },
        {
        "itemId": "12347",
        "scanCode": "",
        "quantityRequested": 5.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.430,
        "quantityFulfilledUnit": "kilograms",
        "replaced": true,
        "replacement": {
            "itemId": "12",
            "shopperProvidedName": "Oranges",
            "shopperProvidedPrice": 1.23
        }
        }
    ],
    "bagsCount": 1
    }
}
```

### ORDER_IN_TRANSIT
Order on its way to the customer.
```json
{
    "eventId": 1201895966044343907,
    "eventName": "order.in.transit",
    "eventTimestamp": "2023-01-12T10:18:12Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeslot": {
        "id": "slot45",
        "fromDate": "2023-01-12T10:00:00+00:00",
        "toDate": "2023-01-12T11:00:00+00:00"
    },
    "shopper": {
        "id": "shopper-01",
        "name": "Lukasz",
        "avatarUrl": "https:\/\/media.lolamarket.com\/shopper\/lsdfdsf-sfdfs123-asd2.jpg"
    },
    "serviceType": "DELIVERY",
    "express": false,
    "articles": [
        {
        "itemId": "12345",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
        },
        {
        "itemId": "12346",
        "scanCode": "00980349941",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": true,
        "replacement": {
            "itemId": "12345"
        }
        },
        {
        "itemId": "12347",
        "scanCode": "",
        "quantityRequested": 5.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.430,
        "quantityFulfilledUnit": "kilograms",
        "replaced": true,
        "replacement": {
            "itemId": "12",
            "shopperProvidedName": "Oranges",
            "shopperProvidedPrice": 1.23
        }
        }
    ],
    "bagsCount": 1
    }
}
```

### ORDER_DELIVERED
Order delivered to the customer.
```json
{
    "eventId": 1201895966044343908,
    "eventName": "order.delivered",
    "eventTimestamp": "2023-01-12T10:43:11Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeslot": {
        "id": "slot45",
        "fromDate": "2023-01-12T10:00:00+00:00",
        "toDate": "2023-01-12T11:00:00+00:00"
    },
    "shopper": {
        "id": "shopper-01",
        "name": "Lukasz",
        "avatarUrl": "https:\/\/media.lolamarket.com\/shopper\/lsdfdsf-sfdfs123-asd2.jpg"
    },
    "serviceType": "DELIVERY",
    "express": false,
    "articles": [
        {
        "itemId": "12345",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
        },
        {
        "itemId": "12346",
        "scanCode": "00980349941",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": true,
        "replacement": {
            "itemId": "12345"
        }
        },
        {
        "itemId": "12347",
        "scanCode": "",
        "quantityRequested": 5.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.430,
        "quantityFulfilledUnit": "kilograms",
        "replaced": true,
        "replacement": {
            "itemId": "12",
            "shopperProvidedName": "Oranges",
            "shopperProvidedPrice": 1.23
        }
        }
    ],
    "bagsCount": 1
    }
}
```

### ORDER_ON_HOLD
Order on hold for some reason that may include:
```json
{
    "eventId": 1201895966044343909,
    "eventName": "order.onHold",
    "eventTimestamp": "2023-01-12T10:34:11Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "timeSlot": {
        "id": "slot1",
        "fromDate": "2023-01-11T14:00:00+00:00",
        "toDate": "2023-01-11T15:00:00+00:00"
    },
    "reason": {
        "code": "CUSTOMER_NO_SHOW",
        "description": "Customer not abailable at delivery location."
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_REJECTED
Order rejected by the OMS for some reason.
```json
{
    "eventId": 1201895966044343910,
    "eventName": "order.rejected",
    "eventTimestamp": "2023-01-11T19:00:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "reason": {
        "code": "TIMESLOT_NOT_AVAILABLE",
        "description": "The timeslot provided is not available."
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_CANCELED
Order has been canceled before left the store. A cancelation could be initiated by the customer, the retailer, the shopper, or the OMS
```json
{
    "eventId": 1201895966044343911,
    "eventName": "order.canceled",
    "eventTimestamp": "2023-01-11T19:00:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "reason": {
        "code": "PICKING_LOCATION_NOT_AVAILABLE",
        "description": "Picking location is not available."
    },
    "serviceType": "DELIVERY",
    "express": false
    }
}
```

### ORDER_RETURNED
Order has been canceled after leaving the store so need to be returned to picking location.
```json
{
    "eventId": 1201895966044343912,
    "eventName": "order.returned",
    "eventTimestamp": "2023-01-12T19:00:00Z",
    "eventPayload": {
    "orderId": "b7fab7ae-11fc-4453-98e1-a2f5421a2b81",
    "pickingLocation": {
        "id": "123",
        "name": "NORTH-21242"
    },
    "reason": {
        "code": "CUSTOMER_NO_SHOW",
        "description": "Customer not abailable at delivery location."
    },
    "serviceType": "DELIVERY",
    "express": false,
    "articles": [
        {
        "itemId": "12345",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false,
        "returned": true
        },
        {
        "itemId": "12346",
        "scanCode": "00980349941",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": true,
        "replacement": {
            "itemId": "12345"
        },
        "returned": true
        },
        {
        "itemId": "12347",
        "scanCode": "",
        "quantityRequested": 5.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.430,
        "quantityFulfilledUnit": "kilograms",
        "replaced": true,
        "replacement": {
            "itemId": "12",
            "shopperProvidedName": "Oranges",
            "shopperProvidedPrice": 1.23
        },
        "returned": true
        }
    ]
    }
}
```