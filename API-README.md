# API Error Codes: A Beginner's Guide

An API lets two programs communicate. An HTTP status code is the API's short way of saying whether a request worked or what went wrong.

Imagine a shopping app asking an online store for an order:

## Client errors: the request needs attention

These codes usually mean the request, login, payment, or requested item needs to be checked.

| Code | Simple meaning | Shopping app example |
| --- | --- | --- |
| **400 Bad Request** | The request is missing information or has invalid data. | The app sends an order with a quantity of `zero` when the API expects a number. |
| **401 Unauthorized** | The request has no valid login credentials. | The user's login token is missing, expired, or invalid. Sign in again or provide a valid token. |
| **402 Payment Required** | Payment is required before the requested action can proceed. | The user needs to pay an outstanding invoice to renew a subscription. This code is reserved and its use depends on the API. |
| **404 Not Found** | The requested API route or item does not exist. | The app asks for order `12345`, but the store cannot find that order. |

## Server errors: the API or a service it depends on has a problem

These codes usually are not fixed by changing the request. The API provider may need to investigate. A retry can help for temporary problems; avoid repeatedly retrying without a delay.

| Code | Simple meaning | Shopping app example |
| --- | --- | --- |
| **500 Internal Server Error** | The API hit an unexpected problem. | The store's order service encountered an error while processing the request. |
| **502 Bad Gateway** | An API gateway received an invalid response from another service. | The store's front door service contacted its inventory service, but got a broken response. |
| **503 Service Unavailable** | The API is temporarily unable to handle requests. | The store is under maintenance or too busy. Try again later; follow a `Retry-After` header if provided. |
| **504 Gateway Timeout** | A gateway did not get a response from another service in time. | The store's front door service waited too long for the inventory service. |

## Quick way to remember

- **400, 401, 402, 404:** Check the request, credentials, payment, or requested item.
- **500, 502, 503, 504:** The API or one of its supporting services has a problem.
- **502 vs. 504:** `502` means the gateway got a bad response; `504` means it waited too long.

Exact behavior can vary between APIs. Check that API's documentation for its error response details and retry guidance.
