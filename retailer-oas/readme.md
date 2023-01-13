 # Discussion points

- [tech] Authentication and Authorization strategy;
  - [product] define flow to send credentials (eg.: clientId and secret) to the retailer;

- [tech] Geographic areas [representation](https://opencagedata.com/guides/how-to-think-about-postcodes-and-geocoding):
  - many countries do not have any form of postal code at all
  - many countries and territories of the world use the postal service of other countries (thus, we might need to ask for the country code along with the postal code)

- Notifications types:
  - Webhooks:
    - [product] define all types of events to be subscribed by the retailer
    - define the best strategy for events subscription:
      a) [tech] /subscribe and /unsubscribe endpoints (or similar)
      b) [product] set up by us, as part o the initial retailer configuration process
  - [product] (?) emails:
    - if so, define all types of emails and its receivers
  - [product] (?) others:

- [tech] Final API data models / schemas / concepts (eg.: for location, fleet, capacity, order, etc)

- [product] Does the time slots availability varies depending on the type of services? Eg.: Availability for pickup vs deliver vs ...
  - (looks like yes)

- [product] Clarify integration/communication points with the Retailer after the moment of order placement (Fulfilment flow)
  - [tech] create endpoints

- [product] Setup flows
  - How are we handling assortment since this API is mostly the "fulfilment flow"?


# TODO: (?) re-think and rename some concepts: eg.: picking-locations to picking-places?
# TODO: review auth token generation - [https://swagger.io/docs/specification/authentication/oauth2/]
# TODO: review revoke token [https://docs.instacart.com/connect/api/oauth/revoke_access_token]
# TODO: POST /picking-locations: bulk or single creation?
