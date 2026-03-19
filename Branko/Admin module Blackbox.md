# Blackbox Testplan: Admin Module (Moderatie & Beheer)

In een blackbox-test wordt de functionaliteit getest zonder dat de interne codestructuur bekend is. We focussen ons op de input, de acties in de interface en de verwachte output.

## 1. Testidentificatie
*   **Module:** Admin Module
*   **Doel:** Verifiëren of moderatie-acties, toegangscontrole en statistieken correct functioneren volgens de functionele eisen.
*   **Preconditie:** Een systeem met bestaande gebruikers, posts en interacties, en een account met 'Admin' rechten.

## 2. Testgevallen

### Testgeval 1: Ongeautoriseerde toegang tot Moderatie Dashboard
*   **Doel:** Controleren of een reguliere gebruiker geen toegang heeft tot admin-functionaliteiten.
*   **Input:** Inloggen met een standaard `UserID` (niet-admin) en navigeren naar de URL van de Admin Module.
*   **Verwachte Actie:** Het systeem weigert toegang.
*   **Verwacht Resultaat:** Foutmelding (bijv. 403 Forbidden) of automatische redirect naar de home-feed. De gebruiker kan geen posts van anderen verwijderen.

### Testgeval 2: Content Moderatie (Verwijderen Post)
*   **Doel:** Controleren of een Admin een ongepaste post kan verwijderen.
*   **Input:** `PostID` van een bestaande post. Klikken op "Verwijderen" in het Moderatie Dashboard.
*   **Verwachte Actie:** De Admin Module stuurt een verwijder-opdracht naar de Post Module.
*   **Verwacht Resultaat:** 
    *   De status van de post verandert naar `Status: Deleted`.
    *   De post is niet meer zichtbaar in de 'Following' feed van de User Module.
    *   De actie wordt opgeslagen in de logs van de Admin Module.

### Testgeval 3: Content Moderatie (Verwijderen Comment)
*   **Doel:** Controleren of een Admin een specifieke reactie kan verwijderen.
*   **Input:** `CommentID` van een ongepaste reactie.
*   **Verwachte Actie:** De Admin Module stuurt een signaal naar de Interaction Module.
*   **Verwacht Resultaat:** De specifieke comment verdwijnt bij de betreffende post. De teller (aantal comments) op de post wordt bijgewerkt.

### Testgeval 4: Spam Preventie (Blokkeren Gebruiker)
*   **Doel:** Controleren of een admin een gebruiker kan blokkeren om verdere spam te voorkomen.
*   **Input:** `UserID` van de vermeende spammer. Selecteer "Blokkeer Gebruiker".
*   **Verwachte Actie:** De Admin Module update de status van de gebruiker in de Storage Module.
*   **Verwacht Resultaat:** De betreffende gebruiker kan niet meer inloggen (Auth Module weigert toegang) en diens bestaande content wordt onzichtbaar.

### Testgeval 5: Statistieken Dashboard Inzien
*   **Doel:** Controleren of de analytics correct worden weergegeven.
*   **Input:** Openen van het Statistieken Dashboard.
*   **Verwachte Actie:** De Admin Module vraagt gegevens op bij de Storage Module (bijv. totaal aantal likes/reacties).
*   **Verwacht Resultaat:** Er wordt een overzicht getoond met kloppende data (bijv. "Post X heeft 50 likes"). Gegevens moeten overeenkomen met de werkelijke data in de Interaction Module.

## 3. Acceptatiecriteria
| ID | Criterium | Resultaat (P/F) |
|:---|:---|:---|
| AC 1 | Alleen accounts met admin-rechten kunnen content van derden verwijderen. | |
| AC 2 | Na verwijdering door een admin krijgt de post/comment de status 'Deleted' in de database. | |
| AC 3 | Verwijderde content is direct onzichtbaar voor reguliere gebruikers. | |
| AC 4 | De moderatie-interface is overzichtelijk en toont alle noodzakelijke metadata (ID's). | |

---
**Legenda:**
*   **P (Pass):** Functionaliteit werkt zoals beschreven.
*   **F (Fail):** Er is een afwijking tussen de verwachte en werkelijke output.