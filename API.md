# BitFreighter API
The BitFreighter API facades the complexity of logistics integrations by providing a standard REST interface that works with all trading partners regardless of their technologies or mapping logic.

https://api.bitfreighter.com

## Authorizing
Once you have a subscription with BitFreighter you can login to the web interface to create an API token.
Don't share this token with anyone, and save it in a safe place.

Using the token is easy.  Just place it in the `Authorization` HTTP header like so:
```
Authorization: Bearer {your-token-here}
```

## Resources
- [Trading Partners](#trading-partners)
    - [list](#list-trading-partners)
    - [create](#create-a-trading-partner)
- [Loads](#loads)
    - [list](#list-loads)
    - [accept](#accept-a-load)
- [Statuses](#statuses)
    - [create](#create-a-status)

### Trading Partners
Trading partners are the companies you do business with.  When you create a trading partner it will start in "pending" status while BitFreighter builds the agreement between your business and the partner.  Once that is complete, the status will change to "active".

#### Fields
| Field  | Type | Description |
| ------------- | ------------- | ------------- |
| id  | integer | uniquely identifies your trading partner  |
| name  | string | display name for your trading partner |
| status | string | (pending/active) |

#### List Trading Partners
##### Request
```
GET https://api.bitfreighter.com/partners
```
##### Response
```
STATUS: 200
{
  "data": [
    { 
      "id": 999, 
      "name": "Example Trading Partner",
      "status": "active"
    },
    ...
  ]
}
```
#### Create a Trading Partner
##### Request
```
POST https://api.bitfreighter.com/partners
BODY
{
  "name": "My Trading Partner"
}
```
##### Response
```
STATUS: 201
{
  "data": {
    "name": "My Trading Partner"
  }
}
```
### Loads
Load in "available" status are analogous to the 204 EDI Carrier Load Tender. They are used by shippers to communicate interest in having goods shipped.

#### Fields
| Field | Type | Description |
| --- | --- | --- |
| id | unique identifier | The BitFreighter identifier for the load |
| status | string | (available, accepted, rejected) |
| TODO | TODO | TODO: need to flesh out the rest of these fields |

#### List Loads
##### Request
```
GET https://api.bitfreighter.com/loads
```
##### Response
```
STATUS: 200
{
  "data": [
    { 
      "id": 999,      
       "status": "status",
       ...
    },
    ...
  ]
}
```
#### Accept a Load
Available loads may be accepted.  BitFreighter will send a 990 EDI (or equivalent) message to the trading partner to communicate the acceptance of this load.
##### Request
```
PATCH https://api.bitfreighter.com/loads/999
{
  "status": "accepted"
}
```
##### Response
```
STATUS: 202
```
### Statuses
Status updates are used to provide information about a load being shipped. 
#### Create a Status
Creating a new status for a load will send a 214 EDI message (or equivalent) to the trading partner to provide information about the load being shipped.
##### Request
```
POST https://api.bitfreighter.com/loads/999/statuses
{
  // TODO flesh out these fields
}
```
##### Response
```
STATUS: 201
{
  "id": 123
}
```
