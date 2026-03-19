# Blogging Platform Integration Test
#### Gemaakt door: Mikhaela Balaga 1ES
#### Groep: Thibau Vranken, Branko Claes, Mikhaela Balaga

# Integratie Test Flow: "The Content Lifecycle & Moderation Path"

**Doel:** Verifiëren dat de interactie tussen de User Module, Post Module en Admin Module vlekkeloos verloopt, inclusief database-integriteit en autorisatie-checks.

## 1. Testfase: User Onboarding & Content Creatie
*Focus: User Module + Post Module*

1.  **Stap 1 (Registratie):** Een nieuwe gebruiker (User B) registreert zich met een geldig e-mailadres.
    *   **Actie:** `POST /api/user/register`.
    *   **Whitebox Check:** Controleer of het wachtwoord gehasht is in de database via Argon2/BCrypt.
2.  **Stap 2 (Post Creatie):** User B maakt een nieuwe blogpost aan met de status 'Published'.
    *   **Actie:** `createPost("Ongepaste Titel", "Ongepaste Content")`.
    *   **Whitebox Check:** Verifieer of de `Post` entiteit correct is gekoppeld aan de `User` ID in de database.

## 2. Testfase: Sociale Interactie & Privacy
*Focus: User Module (Following/Blocking) + Post Module (Feed)*

3.  **Stap 3 (Volgen):** Een bestaande gebruiker (User A) volgt User B.
    *   **Actie:** Klik op 'Volgen' bij User B.
    *   **Whitebox Check:** Controleer of de `target_id` niet gelijk is aan `follower_id`.
4.  **Stap 4 (Blokkeren):** User A vindt de content van User B aanstootgevend en blokkeert User B.
    *   **Actie:** Klik op 'Blokkeer' bij User B.
    *   **Whitebox Check:** Verifieer of de SQL-query voor de feed van User A nu een `LEFT JOIN` bevat op de `blocks` tabel om de content van User B te filteren.

## 3. Testfase: Administratieve Interventie (Moderatie)
*Focus: Admin Module + Post Module + User Module*

5.  **Stap 5 (Ongeautoriseerde Toegang):** User A probeert via de URL direct naar het Admin Dashboard te gaan om de post van User B te verwijderen.
    *   **Actie:** Navigeer naar `/admin/dashboard` als reguliere gebruiker (Blackbox Testgeval 1).
    *   **Whitebox Check:** De `checkUserRole()` functie moet een `UnauthorizedError (403)` gooien (Whitebox Testgeval 1).
6.  **Stap 6 (Moderatie door Admin):** Een Admin logt in en verwijdert de bewuste post van User B.
    *   **Actie:** Klik op "Verwijderen" in het Moderatie Dashboard (Blackbox Testgeval 2).
    *   **Whitebox Check:** Controleer of de database een **Soft Delete** uitvoert (`UPDATE posts SET status = 'Deleted'`) in plaats van een fysieke delete (Whitebox Testgeval 2).

## 4. Testfase: Systeem Integriteit & Rapportage
*Focus: Admin Module (Logging/Stats) + User Module (Account Status)*

7.  **Stap 7 (Audit Logging):** De systeembeheerder controleert of de actie van de Admin is vastgelegd.
    *   **Actie:** Query de `AdminLogs` tabel.
    *   **Whitebox Check:** Er moet exact één record zijn voor de actie `DELETE_POST` met de juiste `adminId` en `targetId` (Whitebox Testgeval 3).
8.  **Stap 8 (Statistieken Aggregatie):** De Admin bekijkt de statistieken om de impact te zien.
    *   **Actie:** Open Statistieken Dashboard (Blackbox Testgeval 5).
    *   **Whitebox Check:** Verifieer of de SQL `COUNT` queries de verwijderde post niet meer meetellen in de actieve posts, maar wel in de totale moderatie-acties (Whitebox Testgeval 5).
9.  **Stap 9 (Account Schorsing):** Omdat User B herhaaldelijk regels overtreedt, blokkeert de Admin het hele account van User B.
    *   **Actie:** Selecteer "Blokkeer Gebruiker" in Admin Module (Blackbox Testgeval 4).
    *   **Verwacht Resultaat:** De Auth Module weigert verdere logins van User B. Content van User B verdwijnt universeel uit alle feeds.

---

## Overzicht van verwachte resultaten (Acceptatie)

| ID | Onderdeel | Verwacht Resultaat |
|:---|:---|:---|
| **INT-01** | Data Flow | De post status flow is: `Draft` -> `Published` -> `Deleted`. |
| **INT-02** | Security | Alleen de Admin kan de status naar `Deleted` wijzigen; User A (regulier) krijgt een 403. |
| **INT-03** | Integriteit | Bij verwijdering van User B (Cascade) moeten volg-relaties verdwijnen (WB-07). |
| **INT-04** | Consistentie | De statistieken in het Admin Dashboard komen 1-op-1 overeen met de records in de Interaction/Post database. |