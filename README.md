"# 31 Days of JavaScrpt Interview Questions"

## Day 1 of 31 days Interview question

### Implement Promises in JavaScript

Implemented basic functionality of Promise

```js
class MeraPromise {
  constructor(executor) {
    this.onSuccess = null;
    this.onFailed = null;
    this.isFullfilled = false;
    this.isRejected = false;
    this.isCalled = false;
    this.value;

    executor(this.resolve, this.reject);
  }

  then(cb) {
    this.onSuccess = cb;
    if (this.isFullfilled && !this.isCalled) {
      this.isCalled = true;
      this.onSuccess(this.value);
    }
    return this;
  }

  catch(cb) {
    this.onFailed = cb;
    if (this.isRejected && !this.isCalled) {
      this.isCalled = true;
      this.onFailed(this.value);
    }
    return this;
  }

  resolve = (successMessage) => {
    this.isFullfilled = true;
    this.value = successMessage;
    if (typeof this.onSuccess === "function") {
      this.onSuccess(successMessage);
    }
  };

  reject = (errorMessage) => {
    this.isRejected = true;
    this.value = errorMessage;
    if (typeof this.onFailed === "function") {
      this.onFailed(errorMessage);
    }
  };

  //Promise.resolve
  static resolve(value) {
    return new MeraPromise((res, rej) => {
      res(value);
    });
  }

  static reject(error) {
    return new MeraPromise((res, rej) => {
      res(error);
    });
  }
}

const myPromise = new MeraPromise((res, rej) => {
  setTimeout(() => {
    res("Promise Resolved");
    // rej("Promise rejected");
  }, 1000);
});

myPromise
  .then((data) => {
    console.log("Then Data", data);
  })
  .catch((err) => {
    console.log("Catch error", err);
  });

const myPromise2 = MeraPromise.resolve("Ho gaya resolve");
myPromise2.then((data) => {
  console.log(data);
});
```
