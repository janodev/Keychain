![Swift](https://github.com/janodev/keychain/workflows/Swift/badge.svg?branch=main)

Keychain wrapper.

Store a value as a generic password:
```swift
let account = "an-arbitrary-string"
let store = ValueKeychainStore(accountName: account)
store.set("some value")
print(store.get()) // prints "some value"
```

Use the ObservedValueStore to react to value changes:
```swift
let underlyingStore = ValueKeychainStore(accountName: account)
let store = await ObservedValueStore(valueStore: underlyingStore)
let observation = await store.observe { [weak self] value in
    print("Value changed to \(value)")
} 
try await store.set("bananas")
observation.stopObserving()
```
