```mermaid
classDiagram
    ClassA <|-- ClassB
    ClassA : +String name
    ClassA : +doSomething()
    class ClassB {
        +int age
        +isAdult() bool
    }