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

### Trading Partners
Trading partners are the companies you do business with.  

#### Fields
| Field  | Type | Description |
| ------------- | ------------- | ------------- |
| id  | integer | uniquely identifies your trading partner  |
| name  | string | display name for your trading partner |
| status | string | (pending/active) A trading partner starts in pending status while BitFreighter builds out the agreement with your partner |

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
