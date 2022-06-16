# Jest

* [Guides](https://jestjs.io/docs/snapshot-testing)
* [API](https://jestjs.io/docs/api)

toBe uses Object.is to test exact equality. If you want to check the value of an object, use toEqual instead, toEqual recursively check every field of an object or array.

## Truthiness

* `toBeNull` matches only `null`
* `toBeUndefined` matches only `undefined`
* `toBeDefined` is the opposite of `toBeUndefined`
* `toBeTruthy` matches anything that an if statement treats as `true`
* `toBeFalsy` matches anything that an if statement treats as `false`

## Regexp

You can check strings against regular expressions with toMatch:

`expect('Christoph').toMatch(/stop/)`

## Asynchronous code

* [Documentation](https://jestjs.io/docs/en/asynchronous)

* Callbacks with done().
* Promises with .resolves / .rejects matchers.
* async / await
* You can combine async and await with .resolves or .rejects.

## Testing promise rejections

* [Error handling](https://jestjs.io/docs/en/tutorial-async#error-handling)

Errors can be handled using the `.catch` method. Make sure to add `expect.assertions` to verify that a certain number of
assertions are called. Otherwise a fulfilled promise would not fail the test.

The.rejects helper works like the `.resolves` helper. 

## Setup, tear down, scoping

* [Documentation](https://jestjs.io/docs/en/setup-teardown#scoping)

If you have some work you need to do repeatedly for many tests, you can use `beforeEach` and `afterEach`.

If you only need to do setup once, at the beginning of a file, use `beforeAll` and `afterAll`.

## Scoping

When they are inside a describe block, the before and after blocks only apply to the tests within that describe block. 

## Control execution flow

Use `.only/.skip` on test or describe blocks

# Snapshots

* [Documentation](https://jestjs.io/docs/en/snapshot-testing)
* [Snapshot testing best practices](https://jestjs.io/docs/en/snapshot-testing#best-practices)

Property Matchers for generated properties like random IDs and dates.

```javascript
expect(user).toMatchSnapshot({
  createdAt: expect.any(Date),
  id: expect.any(Number),
});
```

## Mock Functions

* [Documentation](https://jestjs.io/docs/en/mock-functions)
* [.mock property](https://jestjs.io/docs/en/mock-functions#mock-property)

There are two ways to mock functions: Either by creating a mock function to use in test code, or writing a [manual
mock](https://jestjs.io/docs/en/manual-mocks) to override a module dependency.

## Mock modules

* [Documentation](https://jestjs.io/docs/en/mock-functions#mocking-modules)

* jest.mock('module');
* jest.fn
* mockImplementation
* mockImplementationOnce
* mockReturnThis
* mockName

## Manual Mocks

* [Documentation](https://jestjs.io/docs/en/manual-mocks)

Manual mocks are defined by writing a module in a `__mocks__/` subdirectory immediately *adjacent* to the module. When
we require that module in our tests, explicitly calling `jest.mock('./moduleName')` is *required*.

When mocking Node modules, place mocks into root `__mocks__/` directory adjacent to `node_modules` and they will be
automatically mocked. There's no need to explicitly call `jest.mock('module_name')`.

If we want to mock Node's core modules (e.g.: fs or path), then explicitly calling e.g. `jest.mock('path')` is required,
because core Node modules are not mocked by default.

Scoped modules can be mocked by creating a file in a directory structure that matches the name of the scoped module. 

However, when [automock](https://jestjs.io/docs/en/configuration#automock-boolean) is set to true, the manual mock
implementation will be used instead of the automatically created mock, even if `jest.mock('moduleName')` is not called.

## Create mock from module

* [API](https://jestjs.io/docs/en/jest-object#jestcreatemockfrommodulemodulename)

`jest.createMockFromModule(moduleName)`

Use the automatic mocking system to generate a mocked version of the module for you. This is useful when you want to
create a [manual mock](https://jestjs.io/docs/en/manual-mocks) that extends the automatic mock's behavior.

For TypeScript typings use the `ts-jest/utils` `mocked()` function.

## spyOn

* [API](https://jestjs.io/docs/en/jest-object#jestspyonobject-methodname)

`jest.spyOn(object, methodName)`

Creates a mock function similar to jest.fn but also tracks calls to object[methodName]. Returns a Jest [mock
function](https://jestjs.io/docs/en/mock-function-api). 

## ES6 Classes

* [Documentation](https://jestjs.io/docs/en/es6-class-mocks)

Any mock for an ES6 class must be a function or an actual ES6 class (which is, again, another function). So you can mock
them using [mock functions](https://jestjs.io/docs/en/mock-functions).

## Bypassing mocked modules

* jest.unmock('module')
* jest.requireActual('module')

# [Expect](https://jestjs.io/docs/en/expect)

[Additional Jest matchers](https://github.com/jest-community/jest-extended)

[.toHaveLength(number)](https://jestjs.io/docs/en/expect#tohavelengthnumber)

