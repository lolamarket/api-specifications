# Webhook events for order status tracking

<img src="http://lolamarket.statics.prod.s3.amazonaws.com/lola-help/order_state_machine.jpg" />
    
1. [order.confirmed](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_confirmed) 
2. [order.allocated](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_allocated) 
3. [order.rescheduled](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_rescheduled) 
4. [order.in.picking](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_in_picking) 
5. [order.picked](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_picked) 
6. [order.in.transit](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_in_transit) 
7. [order.delivered](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_delivered) 
8. [order.on.hold](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_on_hold) 
9. [order.rejected](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_rejected) 
10. [order.canceled](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_canceled) 
11. [order.returned](https://github.com/lolamarket/api-specifications/blob/main/retailer-oas/webhooks.md#order_returned)

### ORDER_CONFIRMED

The `order.confirmed` event indicates that the order has been confirmed by the OMS and is waiting for shopper assignment. This event is triggered when the order has been reviewed and approved by the system, and is now ready for the next step in the process. By monitoring the `order.confirmed` event, the system can ensure that orders are processed in a timely and efficient manner.
If the order can not be confirmed instead of receiving this event you will receive `order.rejected`.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.confirmed",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot1",
      "fromDate": "2023-01-11T14:00:00+00:00",
      "toDate": "2023-01-11T15:00:00+00:00"
    },
    "serviceType": "DELIVERY"
  }
}
```

### ORDER_ALLOCATED

`order.allocated` event indicates that an order has been assigned and accepted by a shopper, who can be a picker, a courier or any other resource responsible for fulfilling the order. This event is triggered after the order has been confirmed and it contains information about the assigned shopper, the order ID, the picking location, and the time slot for delivery or pickup. In some cases, the order may be allocated to multiple resources to fulfill the order. The retailer can use this event to track the progress of the order and get a better understanding of when the order will beready for picking.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.allocated",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot1",
      "fromDate": "2023-01-11T14:00:00+00:00",
      "toDate": "2023-01-11T15:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY"
  }
}
```

### ORDER_RESCHEDULED

Order has been rescheduled for a different time slot, and needs to be allocated again. The event provides details about the new time slot assigned to the order, including the start and end times. The picking location, service type, and express status are also included in the payload. Retailers may receive this event if there is a need to reschedule an order due to various reasons such as logistical constraints or shopper availability. The event can help retailers keep track of any changes to order delivery and ensure timely updates to customers.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.rescheduled",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY"
  }
}
```

### ORDER_IN_PICKING

`order.in_picking` is an event triggered when a shopper has started picking items for an order. The event provides information about the picking location, timeslot, and shopper assigned to the order. Additionally, each product in the order has its own status, which will be updated as the shopper picks them. Retailers can use this event to track the progress of their orders and ensure that they are being fulfilled on time.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.inPicking",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY"
  }
}
```

### ORDER_ITEM_PICKED

`order.item.picked` is an event triggered when an item has been picked by the shopper.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.item.picked",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
    "articles": [
      {
        "itemId": "1111",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 2.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
      }
    ]
  }
}
```

### ORDER_ITEM_REPLACED

A product item has been replaced.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.item.replaced",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
    "articles": [
      {
        "itemId": "1111",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 1.0,
        "quantityFulfilledUnit": "unit",
        "replaced": true,
        "replacement": [
          {
            "itemId": "9876",
            "scanCode": "00980349941",
            "quantityFulfilledUnit": "unit",
            "quantityFulfilled": 2
          },
          {
            "itemId": "98761",
            "scanCode": "009803499410",
            "quantityFulfilledUnit": "unit",
            "quantityFulfilled": 1
          }
        ]
      }
    ]
  }
}
```

### ORDER_ITEM_NOT_FOUND

A product item was not found.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.item.notFound",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
    "articles": [
      {
        "itemId": "1111",
        "scanCode": "00980349940",
        "quantityRequested": 2.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 0.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
      }
    ]
  }
}
```

### ORDER_ITEM_ADDED

A new product item has been added to basket.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.item.added",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeslot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "previousTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
    "articles": [
      {
        "itemId": "12345",
        "scanCode": "00980349941",
        "quantityRequested": 0.0,
        "quantityRequestedUnit": "unit",
        "quantityFulfilled": 4.0,
        "quantityFulfilledUnit": "unit",
        "replaced": false
      }
    ]
  }
}
```

### ORDER_PICKED

The `order.picked` event signifies that the shopper has completed picking all the items and is now heading towards the cashier. This event's payload includes essential information related to product-not-found, out-of-stock, and replacements. In the case of replacements, this event payload displays fully replaced products in-line, while partially replaced products are shown as a partial stock-out along with new or additional items in the order. Retailers receive this event to track the shopper's progress and order fulfillment status accurately and to be able to charge the cutomer .

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.picked",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
		"oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
		"shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
		"articles": [
			{
				"itemId": "12345",
				"scanCode": "00980349941",
				"quantityRequested": 3.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "9876",
				"scanCode": "00980349941",
				"quantityRequested": 0.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 2.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "98761", --- Bags Count ---
				"scanCode": "009803499410",
				"quantityRequested": 20.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			}
		]
  }
}
```

### ORDER_IN_TRANSIT

Order on its way to the customer. It has already passed the checkout process successfully.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.inTransit",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
		"oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
		"shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
		"articles": [
			{
				"itemId": "12345",
				"scanCode": "00980349941",
				"quantityRequested": 3.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "9876",
				"scanCode": "00980349941",
				"quantityRequested": 0.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 2.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "98761", --- Bags Count ---
				"scanCode": "009803499410",
				"quantityRequested": 20.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
		]
  }
}
```

### ORDER_DELIVERED

Order delivered to the customer.

```json
{
  "eventId": 1201895966044343902,
  "eventName": "order.picked",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-10T18:31:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
		"oldTimeslot": {
      "id": "slot1",
      "fromDate": "2023-01-11T10:00:00+00:00",
      "toDate": "2023-01-11T11:00:00+00:00"
    },
		"shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "serviceType": "DELIVERY",
		"articles": [
			{
				"itemId": "12345",
				"scanCode": "00980349941",
				"quantityRequested": 3.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "9876",
				"scanCode": "00980349941",
				"quantityRequested": 0.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 2.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "98761", --- Bags Count ---
				"scanCode": "009803499410",
				"quantityRequested": 20.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
		]
  }
}
```

### ORDER_ON_HOLD

Order on hold for some reason that may include:

```json
{
  "eventId": 1201895966044343909,
  "eventName": "order.onHold",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-12T10:34:11Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
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
    "articles": [
			{
				"itemId": "12345",
				"scanCode": "00980349941",
				"quantityRequested": 3.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "9876",
				"scanCode": "00980349941",
				"quantityRequested": 0.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 2.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
			{
				"itemId": "98761", --- Bags Count ---
				"scanCode": "009803499410",
				"quantityRequested": 20.0,
				"quantityRequestedUnit":"unit",
				"quantityFulfilled": 1.0,
				"quantityFulfilledUnit":"unit",
				"replaced": false
			},
		]
  }
}
```

### ORDER_REJECTED

Order rejected by the OMS for some reason.

```json
{
  "eventId": 1201895966044343910,
  "eventName": "order.rejected",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-11T19:00:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "reason": {
      "code": "PICKING_LOCATION_NOT_VALID",
      "description": "Picking location does not match customer's shipping address."
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
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-11T19:00:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "timeSlot": {
      "id": "slot45",
      "fromDate": "2023-01-12T14:00:00+00:00",
      "toDate": "2023-01-12T15:00:00+00:00"
    },
    "shopper": {
      "id": "shopper-01",
      "name": "Lukasz",
      "picture": "https://media.lolamarket.com/shopper/placeholder.jpg"
    },
    "reason": {
      "code": "ORDER_CANCELLED_BY_OPS_MANAGER",
      "description": "This order has been cancelled by operations manager."
    },
    "serviceType": "DELIVERY"
  }
}
```

### ORDER_RETURNED

Order has been canceled after leaving the store so need to be returned to picking location.

```json
{
  "eventId": 1201895966044343912,
  "eventName": "order.returned",
  "eventProvider": "glovo-xl",
  "eventTimestamp": "2023-01-12T19:00:00Z",
  "eventPayload": {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "orderRef": "238120381238",
    "pickingLocation": {
      "id": "123",
      "name": "NORTH-21242"
    },
    "reason": {
      "code": "CUSTOMER_NO_SHOW",
      "description": "Customer not abailable at delivery location."
    },
    "serviceType": "DELIVERY",
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
        "quantityFulfilled": 0.43,
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
