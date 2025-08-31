# User Registration Flowchart

```mermaid
flowchart TD
    A([Start]) --> B[Open Registration Page]
    B --> C[Enter User Details: Name, Email, Password]
    C --> D{Are Details Valid?}
    D -- No --> E[Show Error Message]
    E --> C
    D -- Yes --> F[Save User in Database]
    F --> G[Send Confirmation Email]
    G --> H[Registration Successful]
    H --> I([End])

