sequenceDiagram
    autonumber
    actor User as Gebruiker
    participant Browser
    participant Server
    participant Database

    %% --- STAP 1: WEBSITE LADEN ---
    User->>Browser: Open website
    Browser->>Server: HTTP GET /index.html
    
    alt Server is bereikbaar
        Server-->>Browser: Return HTML page (200 OK)
    else Server Error / Onderhoud
        Server-->>Browser: Return Error HTML (503 Service Unavailable)
        Browser-->>User: Toont "Website tijdelijk offline"
    end

    %% --- STAP 2: INLOGGEN ---
    User->>Browser: Vul inloggegevens in
    Browser->>Server: HTTP POST /login (username, password)

    Server->>Database: Controleer gegevens (Query)
    
    alt Database Verbinding Fout
        Database-->>Server: Connection Timeout / Error
        Server-->>Browser: Return HTML (500 Internal Server Error)
        Browser-->>User: Toont "Er is iets misgegaan, probeer later opnieuw"
    
    else Gegevens gevonden
        Database-->>Server: User gevonden (Hash match?)
        
        alt Inlog Succesvol
            Server-->>Browser: HTTP Redirect naar Dashboard (HTML)
            Browser-->>User: Toont persoonlijk dashboard
        else Inlog Ongeldig (Verkeerd wachtwoord)
            Server-->>Browser: Return Login HTML (401 Unauthorized + Melding)
            Browser-->>User: Toont "Ongeldige gebruikersnaam of wachtwoord"
        end
    end