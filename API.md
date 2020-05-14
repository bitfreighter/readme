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
- [Load Tenders](#load-tenders)

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
```json
{
  "data": [
    { 
      "id": 999, 
      "name": "Example Trading Partner",
      "status": "active"
    }
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
```json
{
  "data": {
    "name": "My Trading Partner"
  }
}
```
### Load Tenders
Load tenders are analogous to the 204 EDI Carrier Load Tender. They are used by shippers to communicate interest in having goods shipped.

#### Fields
| Field | Type | Description |
| --- | --- | --- |
| id | unique identifier | The BitFreighter identifier for the load |
| status | string | (available, accepted, rejected) |
| TODO | TODO | TODO: need to flesh out the rest of these fields |
