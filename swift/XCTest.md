# XCTest

It is the default framework for testing.

Notes based on: [(Improving Your) XCTAssert* Failure Messages](https://www.basbroek.nl/xctassert-asterisk)


## General principles on unit testing

Treat your test code as if it were production code; or at least close to it. If your tests are hard to understand, their value will eventually be impacted. How?

1. make your test's name very explicit: use snake-case in it to separate the function name of given and expected elements
2. use a “given, when, then” strategy for the test content
3. have understandable error messages

```swift
  func test_createEmployeeSetting_givenNetworkingError_shouldForwardResult() {
      // Given
      let exp = expectation(description: "Should forward the error from networking worker")
      networkingWorkerMock.expectedFailureRaw = TurboError("test error")

      // When
      sut.createEmployeeSetting() { (result) in
          switch result {
          case .failure(let error):
              XCTAssert(error.localizedDescription.contains("test error"))
              exp.fulfill()
          default:
              XCTFail("Not testing this case")
          }
      }

      // Then
      wait(for: [exp], timeout: 0.1)
  }
```

## XCTest Assertions and their failure messages

### Nil Assertions
```swift
var myString: String? = nil

XCTAssertNotNil(myString)
// XCTAssertNotNil failed

_ = try XCTUnwrap(myString)
// XCTUnwrap failed: expected non-nil value of type "String"
```

### Equality Assertions
```swift
XCTAssertNotEqual(0.333, 0.666, accuracy: 0.3)
// XCTAssertNotEqualWithAccuracy failed: ("0.333") is equal to ("0.333") +/- ("0.3")
```

### Expected Failure Assertions
```swift
XCTExpectFailure { // Expected failure but none recorded
    XCTAssertFalse(false)
}

XCTExpectFailure {
    XCTAssertFalse(false)
    // Expected failure: XCTAssertFalse failed
}

let options = XCTExpectedFailure.Options()
options.issueMatcher = { issue in
    issue.compactDescription.contains("Hello")
}

XCTExpectFailure(options: options) { // Expected failure but none recorded
    XCTAssertFalse(false, "Hello")
}
```

### Skipping Assertions
```swift
try XCTSkipIf(true)
// Test skipped

try XCTSkipUnless(false)
// Test skipped
```
