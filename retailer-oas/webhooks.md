# Webhook events for order status tracking
<img src="http://lolamarket.statics.prod.s3.amazonaws.com/lola-help/order_state_machine.jpg" />
    
1. [order.received](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_received) 
2. [order.confirmed](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_confirmed) 
3. [order.allocated](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_allocated) 
4. [order.rescheduled](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_rescheduled) 
5. [order.in.picking](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_in_picking) 
6. [order.picked](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_picked) 
7. [order.in.transit](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_in_transit) 
8. [order.delivered](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_delivered) 
9. [order.on.hold](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_on_hold) 
10. [order.rejected](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_rejected) 
11. [order.canceled](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_canceled) 
12. [order.returned](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_returned) 

### ORDER_RECEIVED
`order.received` indicates that an order has been received by the OMS (Order Management System) and is now waiting to be processed. This event is triggered when the order details are successfully captured in the system. The event payload includes all the relevant order information, such as the order ID, picking location ID and name, time slot details, service type, and express delivery status.
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
The `order.confirmed` event indicates that the order has been confirmed by the OMS and is waiting for shopper assignment. This event is triggered when the order has been reviewed and approved by the system, and is now ready for the next step in the process. By monitoring the `order.confirmed` event, the system can ensure that orders are processed in a timely and efficient manner. 
If the order can not be confirmed instead of receiving this event you will receive `order.rejected`.

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
`order.allocated` event indicates that an order has been assigned and accepted by a shopper, who can be a picker, a courier or any other resource responsible for fulfilling the order. This event is triggered after the order has been confirmed and it contains information about the assigned shopper, the order ID, the picking location, and the time slot for delivery or pickup. In some cases, the order may be allocated to multiple resources to fulfill the order. The retailer can use this event to track the progress of the order and get a better understanding of when the order will beready for picking.
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
Order has been rescheduled for a different time slot, and needs to be allocated again. The event provides details about the new time slot assigned to the order, including the start and end times. The picking location, service type, and express status are also included in the payload. Retailers may receive this event if there is a need to reschedule an order due to various reasons such as logistical constraints or shopper availability. The event can help retailers keep track of any changes to order delivery and ensure timely updates to customers.
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
`order.in_picking` is an event triggered when a shopper has started picking items for an order. The event provides information about the picking location, timeslot, and shopper assigned to the order. Additionally, each product in the order has its own status, which will be updated as the shopper picks them. Retailers can use this event to track the progress of their orders and ensure that they are being fulfilled on time.
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
The `order.picked` event signifies that the shopper has completed picking all the items and is now heading towards the cashier. This event's payload includes essential information related to product-not-found, out-of-stock, and replacements. In the case of replacements, this event payload displays fully replaced products in-line, while partially replaced products are shown as a partial stock-out along with new or additional items in the order. Retailers receive this event to track the shopper's progress and order fulfillment status accurately and to be able to charge the cutomer .
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
        "itemId": "1111",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 2.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
        },
        {
        "itemId": "2222",
        "scanCode": "00980349941",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 2.0,
        "quantityFulfilledUnit": "unit",
        "replaced": true,
        "replacement": {
            "itemId": "9999"
        }
        },
        {
        "itemId": "3333",
        "scanCode": "00980349942",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
        },
        {
        "itemId": "4444",
        "scanCode": "",
        "quantityRequested": 5.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.430,
        "quantityFulfilledUnit": "kilograms",
        "replaced": true,
        "replacement": {
            "itemId": "7777"
        }
        },
        {
        "itemId": "5555",
        "scanCode": "",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
        },
        {
        "itemId": "6666",
        "scanCode": "",
        "quantityRequested": 0.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
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
