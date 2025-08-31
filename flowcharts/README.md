# User Registration Flowchart

```mermaid
flowchart TD
    A([Start]) --> B[Open Registration Page]
    B --> C[Enter User Details: Name, Email, Password]
    C --> D{Are Details Valid?}
    D -- No --> E[Show Error Message]
    E --> C
    D -- Yes --> F{Does Email Already Exist?}
    F -- Yes --> G[Show 'Email Already Registered' Message]
    G --> C
    F -- No --> H[Hash Password]
    H --> I[Save User in Database]
    I --> J[Send Confirmation Email]
    J --> K[Registration Successful]
    K --> L([End])


