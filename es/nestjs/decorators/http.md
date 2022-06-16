# HTTP decorators

## @Header()

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/header.decorator.ts)

Request method Decorator. Sets a response header.

For example:
`@Header('Cache-Control', 'none')`

@param name string to be used for header name
@param value string to be used for header value

@see [Headers](https://docs.nestjs.com/controllers#headers)

```typescript
export function Header(name: string, value: string): MethodDecorator;
```

## @HttpCode()

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/http-code.decorator.ts)

Request method Decorator. Defines the HTTP response status code. Overrides default status code for the decorated
request method.

@param statusCode HTTP response code to be returned by route handler.

@see [Http Status Codes](https://docs.nestjs.com/controllers#status-code)

```typescript
export function HttpCode(statusCode: number): MethodDecorator;
```

## @Redirect()

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/redirect.decorator.ts)

Redirects request to the specified URL.

```typescript
export function Redirect(url = "", statusCode?: number): MethodDecorator;
```

## @Render()

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/render.decorator.ts)

Route handler method Decorator. Defines a template to be rendered by the controller.

For example: `@Render('index')`

@param template name of the render engine template file

@see [Model-View-Controller](https://docs.nestjs.com/techniques.mvc)

```typescript
export function Render(template: string): MethodDecorator;
```

## Request methods

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/request-mapping.decorator.ts)

- @Get()
- @Post()
- @Put()
- @Delete()
- @Patch()
- @Options()
- @Head()
- @All()

## Route parameters

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/route-params.decorator.ts)

#### @Request()

Route handler parameter decorator. Extracts the `Request` object from the underlying platform and populates the
decorated parameter with the value of `Request`.

Example: `logout(@Request() req)`

@see [Request object](https://docs.nestjs.com/controllers#request-object)

```typescript
export const Request: () => ParameterDecorator;
```

#### @Response()

Route handler parameter decorator. Extracts the `Response` object from the underlying platform and populates the
decorated parameter with the value of `Response`.

Example: `logout(@Response() res)`

```typescript
export const Response: (options?: ResponseDecoratorOptions) => ParameterDecorator;
```

#### @Next()

Route handler parameter decorator. Extracts reference to the `Next` function from the underlying platform and populates
the decorated parameter with the value of `Next`.

```typescript
export const Next: () => ParameterDecorator;
```

#### @Ip()

Route handler parameter decorator. Extracts the `Ip` property from the `req` object and populates the decorated
parameter with the value of `ip`.

@see [Request object](https://docs.nestjs.com/controllers#request-object)

```typescript
export const Ip: () => ParameterDecorator;
```

#### @Session()

Route handler parameter decorator. Extracts the `Session` object from the underlying platform and populates the
decorated parameter with the value of `Session`.

@see [Request object](https://docs.nestjs.com/controllers#request-object)

```typescript
export const Session: () => ParameterDecorator;
```

#### @UploadedFile()

Route handler parameter decorator. Extracts the `file` object and populates the decorated parameter with the value of
`file`. Used in conjunction with [multer middleware](https://github.com/expressjs/multer) for Express-based
applications.

For example:

```typescript
uploadFile(@UploadedFile() file) {
  console.log(file);
}
```

@see [Request object](https://docs.nestjs.com/techniques/file-upload)

```typescript
function UploadedFile(): ParameterDecorator (+2 overloads)
```

#### @Headers()

Route handler parameter decorator. Extracts the `headers` property from the `req` object and populates the decorated
parameter with the value of `headers`.

For example: `async update(@Headers('Cache-Control') cacheControl: string)`

@param property name of single header property to extract.

@see [Request object](https://docs.nestjs.com/controllers#request-object)

```typescript
export const Headers: (property?: string) => ParameterDecorator;
```

#### @Query()

Route handler parameter decorator. Extracts the `query` property from the `req` object and populates the decorated
parameter with the value of `query`. May also apply pipes to the bound query parameter.

For example:

```typescript
async find(@Query('user') user: string)
```

@param property name of single property to extract from the `query` object
@param pipes one or more pipes to apply to the bound query parameter

@see [Request object](https://docs.nestjs.com/controllers#request-object)

```typescript
function Query(): ParameterDecorator (+2 overloads)
```

#### @Body()

Route handler parameter decorator. Extracts the entire `body` object property, or optionally a named property of the
`body` object, from the `req` object and populates the decorated parameter with that value. Also applies pipes to the
bound body parameter.

For example:

```typescript
async create(@Body('role', new ValidationPipe()) role: string)
```

@param property name of single property to extract from the `body` object
@param pipes one or more pipes - either instances or classes - to apply to the bound body parameter.

@see [Request object](https://docs.nestjs.com/controllers#request-object)
@see [Working with pipes](https://docs.nestjs.com/custom-decorators#working-with-pipes)

```typescript
function Body(): ParameterDecorator (+2 overloads)
```

#### @Param()

Route handler parameter decorator. Extracts the `params` property from the `req` object and populates the decorated
parameter with the value of `params`. May also apply pipes to the bound parameter.

For example, extracting all params:

```typescript
findOne(@Param() params: string[])
```

For example, extracting a single param:

```typescript
findOne(@Param('id') id: string)
```

@param property name of single property to extract from the `req` object
@param pipes one or more pipes - either instances or classes - to apply to the bound parameter.

@see [Request object](https://docs.nestjs.com/controllers#request-object)
@see [Working with pipes](https://docs.nestjs.com/custom-decorators#working-with-pipes)

```typescript
function Param(): ParameterDecorator (+2 overloads)
```

#### @HostParam()

Route handler parameter decorator. Extracts the `hosts` property from the `req` object and populates the decorated
parameter with the value of `params`. May also apply pipes to the bound parameter.

For example, extracting all params:

```typescript
findOne(@HostParam() params: string[])
```

For example, extracting a single param:

```typescript
findOne(@HostParam('id') id: string)
```

@param property name of single property to extract from the `req` object

@see [Request object](https://docs.nestjs.com/controllers#request-object)

```typescript
function HostParam(): ParameterDecorator (+1 overload)
```

## [@Sse()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/sse.decorator.ts)

Declares this route as a Server-Sent-Events endpoint.

```typescript
export function Sse(path?: string): MethodDecorator;
```
