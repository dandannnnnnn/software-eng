# Whitebox Testplan: Admin Module (Moderatie & Beheer)

In dit testplan focussen we op de interne code-paden, de API-endpoints en de integriteit van de data-flow tussen de Admin Module en de Storage/Post Modules.

## 1. Testidentificatie
*   **Module:** Admin Module (Intern)
*   **Doel:** Verifiëren van de correcte werking van de programmeerlogica, autorisatie-checks en database-transacties.
*   **Focus:** Controlestructuren (`if/else`), database-integriteit en foutafhandeling (`try/catch`).

## 2. Whitebox Testgevallen

### Testgeval 1: Autorisatie Logica (RBAC)
*   **Doel:** Controleren of de functie `checkUserRole()` correct onderscheid maakt tussen rollen.
*   **Code-pad:** 
    ```javascript
    if (user.role !== 'ADMIN') { throw new UnauthorizedError(); }
    ```
*   **Input:** Een sessie-token van een `User` met attribuut `role: "MODERATOR"` (in plaats van ADMIN).
*   **Verwachte Actie:** De functie moet de `UnauthorizedError` triggeren.
*   **Verwacht Resultaat:** De code stopt de uitvoering vóórdat de `delete`-functie wordt aangeroepen.

### Testgeval 2: Database Status Transitie (SQL/ORM)
*   **Doel:** Verifiëren of de database-query de status daadwerkelijk wijzigt naar 'Deleted' in plaats van de rij fysiek te verwijderen (Soft Delete).
*   **Query Check:** 
    `UPDATE posts SET status = 'Deleted', deleted_at = NOW() WHERE post_id = ?`
*   **Input:** `AdminModule.deletePost(postID: 501)`
*   **Verwachte Actie:** Controleer de rij in de tabel `Posts` na uitvoering.
*   **Verwacht Resultaat:** De kolom `status` moet de waarde `'Deleted'` bevatten. De post mag niet fysiek uit de database verdwenen zijn (ten behoeve van audit logs).

### Testgeval 3: Logging van Moderatie-acties
*   **Doel:** Controleren of elke admin-actie een log-entry genereert (zoals gespecificeerd in `Functionaliteit.md`).
*   **Code-pad:** 
    ```javascript
    await db.AdminLogs.create({ adminId, action: 'DELETE_POST', targetId: postID, timestamp: Date.now() });
    ```
*   **Input:** Uitvoeren van een verwijder-actie op een comment.
*   **Verwachte Actie:** Een `INSERT`-commando naar de `AdminLogs` tabel.
*   **Verwacht Resultaat:** Na de actie moet een query `SELECT * FROM AdminLogs WHERE targetId = [CommentID]` precies één record teruggeven met de juiste `adminId`.

### Testgeval 4: Foutafhandeling bij niet-bestaande ID's
*   **Doel:** Verifiëren hoe de module omgaat met ongeldige invoer die door de validatielaag glipt.
*   **Input:** `AdminModule.deletePost(postID: -1)` of `null`.
*   **Verwachte Actie:** De code moet een `EntityNotFoundException` of `404` gooien zonder de database te crashen.
*   **Verwacht Resultaat:** De applicatie blijft draaien; de fout wordt gelogd in de error-logs van de server.

### Testgeval 5: Data Aggregatie (Statistieken Dashboard)
*   **Doel:** Controleren of de SQL-aggregatie voor het dashboard correcte berekeningen maakt.
*   **Logic Check:** 
    `SELECT COUNT(*) FROM likes WHERE post_id = ?`
*   **Input:** Openen van statistieken voor een post met 5 likes en 2 comments.
*   **Verwachte Actie:** De code moet twee aparte queries uitvoeren naar de `Interactions` tabel.
*   **Verwacht Resultaat:** Het geretourneerde JSON-object moet exact de waarden `{ likes: 5, comments: 2 }` bevatten.

## 3. Structurele Dekking (Coverage)
*   **Statement Coverage:** Worden alle lijnen in de `AdminController` geraakt?
*   **Branch Coverage:** Worden zowel de `if (isAdmin)` als de `else` paden getest?
*   **Path Coverage:** Worden alle mogelijke scenario's (o.a. mislukte database-verbinding tijdens moderatie) afgedekt?

---

**Tools voor uitvoering:**
*   **Unit Testing:** Jest / Mocha (voor de logica).
*   **DB Testing:** SQL queries om de staat van de Storage Module te controleren.
*   **Mocking:** Het simuleren van de `Post Module` om te zien of de Admin Module de juiste commando's verstuurt.