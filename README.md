# Sourcery - CodeGen Templates

# Model Builders
Code gen Model Builders for Unit tests. 

example:
```
extension User: AutoTestBuilder {
    static private let nameTestDefault = "A"
}

// sourcery:inline:User.AutoTestBuilder
// GENERATED CODE - changes done will be overwritten
final class UserBuilder {
    private var name: String = "A" 

    func with(name: String) -> UserBuilder {
        self.name = name
        return self
    }

    func build() throws -> User {
        guard let name = self.name else { throw AutoTestBuilderError.missingValue("name") }
        return User(
            name:name
        )
    }
}
// sourcery:end
```

# API Client Spy
Code gen API Client Spy

example:
AutoAPISpyable.generated.swift
```
// Generated using Sourcery 1.0.2 — https://github.com/krzysztofzablocki/Sourcery
// DO NOT EDIT

@testable import HelloBuilderCodeGen
final class MessagesAPISpy: MessagesAPI {

    enum Call {
        case fetchAll
        case message
    }
    var calls: [Call] = []

    var fetchAllResult: Result<[Message], APIError>?
    var messageResult: Result<Message, APIError>?

    func fetchAll(completion: (Result<[Message], APIError>) -> Void) {
        calls.append(.fetchAll)
        completion(fetchAllResult ?? .failure(.other))
    }
    func message(id: String, completion: (Result<Message, APIError>) -> Void) {
        calls.append(.message)
        completion(messageResult ?? .failure(.other))
    }
}
```
