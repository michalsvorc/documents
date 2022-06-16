# Gateway

- [What is Amazon API Gateway? - Amazon API
  Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)

## Description

Amazon API Gateway is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and
WebSocket APIs at any scale.

API Gateway handles all the tasks involved in accepting and processing API calls, including traffic management, CORS
support, authorization and access control, throttling, monitoring, and API version management.

- run multiple versions of the same API simultaneously with API Gateway
- take advantage of the global network of edge locations using Amazon CloudFront
- throttle traffic and authorize API calls to ensure that backend operations withstand traffic spikes and backend
  systems are not unnecessarily called.
- API Gateway offers native OIDC and OAuth2 support. To support custom authorization requirements, you can execute a
  Lambda authorizer from AWS Lambda.

## API Types

RESTful APIs:

- [HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
- [REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)

HTTP APIs are the best way to build APIs for a majority of use cases—they're up to 71% cheaper than REST APIs. If your
use case requires API proxy functionality and management features in a single solution, you can use REST APIs.

WEBSOCKET APIs:

- [WebSocket APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-overview.html)
