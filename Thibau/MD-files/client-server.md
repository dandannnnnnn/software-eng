**SUCCESSVOLLE COMMUNICATIE**
sequenceDiagram – Successful Login
    participant User
    participant Browser
    participant Server
    participant Database

    User->>Browser: Open website
    Browser->>Server: HTTP GET /index.html
    Server-->>Browser: Return HTML page

    User->>Browser: Fill login form
    Browser->>Server: HTTP POST /login (username, password)

    Server->>Database: Verify credentials
    Database-->>Server: Valid credentials

    Server-->>Browser: HTML dashboard page: error 200
    Browser-->>User: Show dashboard

**ONSUCCESVOLLE COMMUNICATIE**
sequenceDiagram – Failed Login
    participant User
    participant Browser
    participant Server
    participant Database

    User->>Browser: Open website
    Browser->>Server: HTTP GET /index.html
    Server-->>Browser: Return HTML page

    User->>Browser: Fill login form
    Browser->>Server: HTTP POST /login (username, password)

    Server->>Database: Verify credentials
    Database-->>Server: Invalid credentials

    Server-->>Browser: HTML login error page: error code 401
    Browser-->>User: Show error message