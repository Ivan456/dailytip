Always call `clock.restore()` while using `sinon` package. Your tests may still pass, but forgetting this will likely lead to unobvious errors in future tests which relies on `Date`, `setTimeout`, etc. It happens because `useFakeTimers` modifies global objects thus affecting literally all tests.

```js
describe('My sexy test', function () {
  beforeEach(function () {
    this.clock = sinon.useFakeTimers();
  });

  afterEach(function () {
    this.clock.restore(); // this is essential!
  });
});
```
