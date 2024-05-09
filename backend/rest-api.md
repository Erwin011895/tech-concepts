# REST API

## Dissertation

https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm 

## Effective API design

1. easy to use
2. hard to misuse
3. Complete & concise

## Naming

- use nouns
- leverage logical grouping ( e.g. /orders/customers )
- use plurarized nouns
- collection is a group of resources. `/orders`, `/orders/1`
- use hypens for readability `/inventory-management`
- Version the APIs. `/v1/store` , `/store?version=2`

## HATEOAS

embed links in response

```json
{
    "links": {
        "rel": "customer",
        "href": "https://example.com/customer/99",
        "action": "GET",
        "types": ["text/xml", "aplication/json"]
    }
}
```

## Fiter, Sort, Pagination

### Filter by specific key-values

`/customers?lastname=Doe&age=40`

### Filter only specific keys

`/customers?fields=lastname,age`

### limit the number of items in response

`/customers?limit=50`

### Paginate

`/customers?start=50&limit=50`

### Sort by specific key-value

`/customers?sort=lastname,created_at`

`/customers?sort=+lastname,-created_at` // asc or desc

## Idempotency

- route should not rely on side-effects
- same request for the same resource should result in same state
- http codes may differ
- 1st delete return 204 no content; 2nd delete return 404 not found.

## Async Request

let `POST /orders/create` take 5 minute to finish. Do it async & immediately return 202 (Accepted) with response contain order ID.

create `GET /orders/status/99`. Return `200 OK`

```json
{
    "status": "in progress",
    "links": {
        "rel": "cancel",
        "method": "delete",
        "href": "/orders/status/99"
    }
}
```

When order completed, return `303 See Other` & redirect to next API.

```json
{
    "status": "completed",
    "links": {
        "rel": "location",
        "method": "get",
        "href": "/orders/99"
    }
}
```

## Error code

- Endpoint user need to know what went wrong to be able to fi the request.
- return correct HTTP status code like 204 No Content, 404 Not Found, 422 Unprocessable Entity.

## Security

- SSL / TLS encryption
- Authorization
- implement ACL (access control list)
- rate-limiting, throttling, IP blacklist, preventting XSS

## Documentation

generate docs with tools

- swagger https://swagger.io/
