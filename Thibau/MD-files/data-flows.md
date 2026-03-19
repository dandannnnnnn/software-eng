# Module Communicatie & Data Flow

## Overzicht van module-interacties

| Van Module          | Naar Module       | Input Data                          | Output / Actie                                      |
|--------------------|-------------------|--------------------------------------|-----------------------------------------------------|
| Gebruiker           | Auth Module        | Gebruikersnaam, Wachtwoord             | Sessie-token of foutmelding                          |
| Auth Module         | Storage Module      | Gehashed wachtwoord, Email             | Bevestiging van opslag in DB                          |
| User Module         | Post Module          | UserID, Geboortedatum                   | Toegang tot 18+ content (True/False)                  |
| Post Module         | Storage Module        | Tekst, Media-bestand, Metadata          | PostID en opgeslagen URL's                            |
| Interaction Module  | Post Module           | PostID, Comment tekst, Like-actie        | Update van teller/lijst op de post                    |
| Storage Module       | Interaction Module    | Zoekterm (String)                       | Lijst met matches (Posts/Users)                       |
| Admin Module         | Post/Interaction       | PostID of CommentID                     | Verwijder-opdracht (Status: Deleted)                   |
| Post Module           | User Module            | UserID (Volger)                          | Gefilterde feed gebaseerd op 'Following'               |

---

## Uitleg

- **Gebruiker → Auth Module**  
  De gebruiker logt in met gebruikersnaam en wachtwoord. De Auth Module geeft een sessietoken of een foutmelding terug.

- **Auth Module → Storage Module**  
  Gegevens zoals een gehashed wachtwoord en e-mailadres worden opgeslagen in de database.

- **User Module → Post Module**  
  Op basis van de leeftijd (Geboortedatum) krijgt de gebruiker toegang tot 18+ content of niet.

- **Post Module → Storage Module**  
  Posts met tekst, media en metadata worden opgeslagen en krijgen een unieke PostID.

- **Interaction Module → Post Module**  
  Interacties zoals likes en comments updaten de postgegevens.

- **Storage Module → Interaction Module**  
  Zoeken in de database levert een lijst met relevante posts of gebruikers.

- **Admin Module → Post/Interaction**  
  Administrators kunnen posts of reacties verwijderen.

- **Post Module → User Module**  
  Gebruikers die anderen volgen krijgen een gefilterde feed.