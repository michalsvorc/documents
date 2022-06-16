# API Gateway

- [Documentation](https://docs.aws.amazon.com/apigateway/index.html)
- [Concepts](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-basic-concept.html)
- [Amazon API Gateway tutorials and workshops](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-tutorials.html)
- [API Gateway Amazon Resource Name (ARN) reference](https://docs.aws.amazon.com/apigateway/latest/developerguide/arn-format-reference.html)

Examples:

- [Amazon API Gateway Developer Guide](https://github.com/awsdocs/amazon-api-gateway-developer-guide/tree/main/cloudformation-templates)

Amazon API Gateway is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and
WebSocket APIs at any scale.

Together with AWS Lambda, API Gateway forms the app-facing part of the AWS serverless infrastructure. For an app to call
publicly available AWS services, you can use Lambda to interact with required services and expose Lambda functions
through API methods in API Gateway.

Integrations:

- [Developer portal](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-developer-portal.html) for publishing your APIs.
- [CloudTrail](https://docs.aws.amazon.com/apigateway/latest/developerguide/cloudtrail.html) logging and monitoring of API usage and API changes.

## API types

- [Choosing between HTTP APIs and REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)

### HTTP APIs

- [Working with HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)

HTTP APIs enable you to create RESTful APIs with lower latency and lower cost than REST APIs. HTTP APIs support OpenID
Connect and OAuth 2.0 authorization. They come with built-in support for cross-origin resource sharing (CORS) and
automatic deployments.

### REST APIs

- [Working with REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html)
- [https://docs.aws.amazon.com/apigateway/api-reference/](https://docs.aws.amazon.com/apigateway/api-reference/)

API Gateway REST APIs use a request/response model where a client sends a request to a service and the service responds
back synchronously. This kind of model is suitable for many different kinds of applications that depend on synchronous
communication.

An API Gateway REST API is made up of resources and methods. A resource is a logical entity that an app can access
through a resource path. A method corresponds to a REST API request that is submitted by the user of your API and the
response returned to the user.

#### Integrations

- [Integrations](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-integration-settings.html)
- [Lambda-Proxy vs Lambda Integration](https://medium.com/@lakshmanLD/lambda-proxy-vs-lambda-integration-in-aws-api-gateway-3a9397af0e6d)

After setting up an API method, you must integrate it with an endpoint in the backend. A backend endpoint is also
referred to as an integration endpoint and can be a Lambda function, an HTTP webpage, or an AWS service action.

- [Lambda proxy integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-cross-account-lambda-integrations.html)

This is a simple, but powerful integration. All the request to the APIGateway URL is forwarded straight to the Lambda
and the response is sent from Lambda. i.e No modifications to the request(query params, body, variables) and
response(status code, message) are done by the APIGateway.

The event parameter has the whole request object sent from the client.

API Gateway has no part in the transmission data. Status code of the response message such as 2XX, 4XX & 5XX are set by
the lambda.

Proxy integrations cannot be configured to transform responses.

- [Lambda non-proxy integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/getting-started-lambda-non-proxy-integration.html)

This is complex, but offers more control over transmission data. The request can be modified before it is sent to lambda
and the response can be modified after it is sent from lambda. This can be done by mapping templates which transforms
the payload, as per the user customisations.

In Lambda non-proxy integration, you must ensure that input to the Lambda function is supplied as the integration
request payload. This implies that you, as an API developer, must map any input data the client supplied as request
parameters into the proper integration request body.

API Gateway has full control of the request has no part in the transmission data.

Status Code of the response message are set by the API Gateway.

The API Gateway passes the input to the Lambda function from the client as the integration request body. The event
object of the Lambda function handler is the input.

- [HTTP proxy integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-create-api-as-simple-proxy-for-http.html)

HTTP proxy integration is a simple, powerful, and versatile mechanism to build an API that allows a web application to
access multiple resources or features of the integrated HTTP endpoint, for example the entire website, with a
streamlined setup of a single API method.

- [HTTP non-proxy integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-create-api-step-by-step.html)

### WebSocket APIs

- [Working with REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api.html)

In a WebSocket API, the client and the server can both send messages to each other at any time. Backend servers can
easily push data to connected users and devices, avoiding the need to implement complex polling mechanisms.

## Error handling

API Gateway treats all invocation and function errors as internal errors. If the Lambda API rejects the invocation
request, API Gateway returns a 500 error code. If the function runs but returns an error, or returns a response in the
wrong format, API Gateway returns a 502 error code. To customize the error response, you must catch errors in your code
and format a response in the required format.

We recommend using AWS X-Ray to determine the source of an error and its cause. X-Ray allows you to find out which
component encountered an error, and see details about the errors. The following example shows a function error that
resulted in a 502 response from API Gateway.
