# Flowchart: User Registration Process

This flowchart illustrates the steps involved in a user registering for the ALX Airbnb system.

## Diagram (Mermaid)

```mermaid
flowchart TD
    A([Start]) --> B[Enter registration details]
    B --> C[Validate input fields]
    C -->|Invalid| D[Show error message]
    D --> B
    C -->|Valid| E[Check if email exists in DB]
    E -->|Exists| F[Show 'Email already exists']
    F --> B
    E -->|Does not exist| G[Hash password & store in DB]
    G --> H[Send confirmation email]
    H --> I([Registration successful])
    I --> J([End])
## File
- `data-flow-diagram.png`: Flow chart representation
