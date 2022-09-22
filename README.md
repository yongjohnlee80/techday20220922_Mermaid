#### 2022/09/22 
# Tech Day : Mermaid Diagram

## 1. Purpose

##### Exploring markdown compatible diagram rendering tools that meets certain requirements.

## 2. Requirements

##### a. Must be able to implement in '.md' file.
##### b. Must be able to render various UML diagrams related to software testing and documentations.
##### c. Nice to have Github integration.
##### d. Nice to have low overhead.

## 3. Mermaid

##### There are two available diagram-rendering engines available for markdown documents, namely the PlantUML and Mermaid engines. However, PlantUML requires heavier resources (its own Java based rendering engine), and is not supported in the GitHub repository file viewers. Mermaid, on the other hand, is based on Javascript and requires less resources to work with, and have Github integration by default.

## 4. Use-cases for Testing

##### Mermaid's requirement diagram display software or testing requirements easily and satisfying elements in easy to understandable syntax.

```mermaid
sequenceDiagram
    autonumber
    loop Smoke Testing
        LM-UI->>Cypress Testing: begins smoke testings
        Cypress Testing-->>Cypress Testing: execute test cases while simulating user interactions
        Cypress Testing-->>LM-UI: PASS!
        Note right of Cypress Testing: Run negative tests too!
    end

        LM-UI->>LM-Backend: Establish connection

    loop Regression Testing
        LM-UI ->> Cypress Testing: begin regression testings
        Cypress Testing -->> Cypress Testing: execute test cases via intercepting requests.

        Cypress Testing->>LM-Backend: send requests
        LM-Backend-->>Cypress Testing: receive response
        Cypress Testing -->> Cypress Testing: verify responses with requests
        Cypress Testing-->>LM-UI: PASS!
    end

```

```mermaid
classDiagram
    Animal <|-- Duck
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
    class Fish{
        -int sizeInFeet
        -canEat()
    }
    class Zebra{
        +bool is_wild
        +run()
    }
```


```mermaid
requirementDiagram

    requirement test_req {
    id: 1
    text: the test text.
    risk: high
    verifymethod: test
    }

    functionalRequirement test_req2 {
    id: 1.1
    text: the second test text.
    risk: low
    verifymethod: inspection
    }

    performanceRequirement test_req3 {
    id: 1.2
    text: the third test text.
    risk: medium
    verifymethod: demonstration
    }

    interfaceRequirement test_req4 {
    id: 1.2.1
    text: the fourth test text.
    risk: medium
    verifymethod: analysis
    }

    physicalRequirement test_req5 {
    id: 1.2.2
    text: the fifth test text.
    risk: medium
    verifymethod: analysis
    }

    designConstraint test_req6 {
    id: 1.2.3
    text: the sixth test text.
    risk: medium
    verifymethod: analysis
    }

    element test_entity {
    type: simulation
    }

    element test_entity2 {
    type: word doc
    docRef: reqs/test_entity
    }

    element test_entity3 {
    type: "test suite"
    docRef: github.com/all_the_tests
    }


    test_entity - satisfies -> test_req2
    test_req - traces -> test_req2
    test_req - contains -> test_req3
    test_req3 - contains -> test_req4
    test_req4 - derives -> test_req5
    test_req5 - refines -> test_req6
    test_entity3 - verifies -> test_req5
    test_req <- copies - test_entity2
```

