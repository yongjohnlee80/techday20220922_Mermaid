#### 2022/09/22 
# Tech Day : Mermaid Diagram

## 1. Purpose

#### Exploring markdown compatible diagram rendering tools that meets certain requirements.

## 2. Requirements

#### a. Must be able to implement in '.md' file.
#### b. Must be able to render various UML diagrams related to software testing and documentations.
#### c. Nice to have Github integration.
#### d. Nice to have low overhead.

## 3. Mermaid

#### There are two available diagram-rendering engines available for markdown documents, namely the PlantUML and Mermaid engines. However, PlantUML requires heavier resources (its own Java based rendering engine), and is not supported in the GitHub repository file viewers. Mermaid, on the other hand, is based on Javascript and requires less resources to work with, and have Github integration by default.

## 4. Use-cases for Testing

#### * Login Page Test Sequences


```mermaid
sequenceDiagram
    autonumber
    participant A as LM-UI
    participant B as Cypress Testing
    participant C as LM-Backend

    Note over A, C: Label Manager Build Begins

    loop Initiates Smoke Testing
        B->>A: executes each test case
        Note over A,B: Simulate User actions
        A-->>B: LM_UI responds to each case
        Note over B: Verify each Response
        B->>C: send request if necessary
        C-->>A: send response
        B->>A: verify HTML layout
        B->>B: log result
        Note right of B: Test Terminates on critical error
    end

        Note over A, C: Regression and Integration Begins

    loop Initiates Regression Testing
        B->>C: executes each test case
        Note over B,C: Make HTTP requests
        C-->>A: Response back to LM-UI
        Note over B: Intercepts response if necessary
        B->>A: verify HTML layout
        B->>B: log result
        Note right of B: Test terminates on critical error
    end

    Note over A, C: Deploy Label Manager

```

#### * Page Object Model Pattern Example


```mermaid
classDiagram
    LoginTestcases *-- LoginPage
    LoginTestcases *-- Verify
    LoginTestcases: verify login with
    LoginTestcases : +(correct credential)
    LoginTestcases : -(invalid input fields)
    LoginTestcases : -(invalid credentials)

    <<Service>> LoginPage
    class LoginPage{
        encapsulate user actions
        type(email/password)
        click(login-button)
    }

    <<Service>> Verify
    class Verify{
        verify results
        verifyHttpResponse()
        verifyErrorMessage()
    }
```

#### * Testing Flow Chart


```mermaid
flowchart TD
    O[Start Build Process]-->Q[Initiate QA Process]
    Q -->A
    A[Execute a test case] --> B{Did it pass?}
    B -->|Yes| C{are there more cases?}
    B -->|No| D[Log error]
    C -->|Yes| A
    C -->|No| E[Deploy Application]
    D -->F{Is it critical?}
    F -->|No| A
    F -->|Yes|G[Terminate Build Process]

```

