# Software Requirements Specification (SRS) - Simple Blogging Platform

## Project
Dit document beschrijft de requirements voor een **simple blogging platform**. Het project heeft als doel een gebruiksvriendelijke omgeving te bieden waar gebruikers accounts kunnen aanmaken, berichten kunnen posten, media kunnen delen en interactie kunnen hebben via likes en comments. De afspraken in dit document geven weer wat de klant verwacht en wat de developer zal opleveren.

Het systeem richt zich op:
* publiceren van blogposts
* interactie tussen gebruikers
* veilige opslag en beheer van content
* gebruiksvriendelijke interface
* basis moderatie en beveiliging

---

### Rollen:
* **Auteur**
* **Lezer**
* **Administrator**

---

## Niet-functionele requirements

### Gebruiksvriendelijkheid
* Interface moet intuïtief zijn en geschikt voor beginners.
* Responsieve layout (bruikbaar op desktop en mobiel).
* Duidelijke foutmeldingen en feedback bij acties.
* Consistente navigatie.

### Performance
* Pagina’s laden binnen een acceptabele tijd (<2 seconden waar mogelijk).
* Feed en zoekfuncties moeten efficiënt data ophalen.
* Media moet geoptimaliseerd worden bij upload.

### Data en opslag 
* Gebruik van relationele database voor gebruikers en posts.
* Media wordt opgeslagen in een veilige directory of cloudoplossing.
* Het systeem ondersteunt geautomatiseerde back-ups die minstens elke 24 uur worden uitgevoerd.
* Data validatie aan zowel client- als serverzijde.
* Encryptie: Alle gevoelige gebruikersdata (PII) wordt in rust versleuteld met industrie-standaard algoritmen.
* Encryptie in transit: Alle dataverkeer verloopt via beveiligde verbindingen (bijv. TLS).

### Beveiliging (Uitgebreid conform industriestandaarden)

#### 1. Authenticatie & Sessiebeheer
* Wachtwoorden worden gehasht (salted hashing) opgeslagen.
* Het systeem dwingt wachtwoorden af met een minimale lengte van 12 tekens en vereist ten minste drie karakterklassen.
* Ondersteuning voor Multi-factor Authentication (MFA) bij gevoelige operaties.
* Accounts worden vergrendeld na meerdere mislukte inlogpogingen.
* Sessies worden veilig aangemaakt. Gebruikerssessies eindigen automatisch na 15 minuten inactiviteit. Er is bescherming tegen session hijacking en fixation.
* Ondersteuning voor SSO (bijv. Google/GitHub login).

#### 2. Autorisatie en Toegangsbeheer
* Toepassing van Role-Based Access Control (RBAC) en het principe van de minste privileges.
* Strikt onderscheid tussen acties voor Auteurs, Lezers en Administrators.
* Alleen gebruikers met de rol "Administrator" kunnen systeeminstellingen wijzigen.
* Toegangscontroles zijn aanwezig op alle API’s en backend services.

#### 3. Input Validatie en Output Handling
* Validatie van alle gebruikersinput tegen SQL injection, Cross-site scripting (XSS), command injection en path traversal.
* Gebruik van geparametriseerde queries voor database-interactie.
* Output encoding voor web-interfaces om onveilige scripts te blokkeren.

#### 4. Logging, Monitoring & Audit
* Registratie van inlogpogingen (inclusief IP en tijdstip), administratieve acties en systeemfouten. Logs zijn bestand tegen manipulatie.
* Het systeem onderhoudt een onwijzigbaar audit-traject voor kritieke transacties.
* Voldoen aan privacywetgeving (zoals GDPR/AVG) inclusief dataminimalisatie en het recht van de gebruiker op toegang of verwijdering van data.

### Onderhoudbaarheid & Veilig Ontwikkelen
* Code moet modulair en documenteerbaar zijn.
* Database schema duidelijk en uitbreidbaar.
* Gebruik van veilige coderingsstandaarden en dependency scanning op kwetsbaarheden.

---

## Activiteit: Aanmelden
#### MVP
* Als viewer en author wil ik een account kunnen aanmaken zodat ik kan bijdragen.
  * Acceptatie: formulier met e-mail, gebruikersnaam en wachtwoord (min. 12 tekens); bevestigingsemail (optioneel).
  * Acceptatie: invoervalidatie en duidelijke foutmeldingen.
  * Acceptatie: Gebruikersconsent management voor privacyvoorwaarden.

---

## Activiteit: Inloggen (auteur en lezer)
#### MVP
* Als geregistreerde gebruiker wil ik kunnen inloggen met gebruikersnaam en wachtwoord zodat ik toegang krijg.
  * Acceptatie: loginformulier valideert credentials; succesvolle/onsuccesvolle melding.
  * Acceptatie: sessie wordt veilig aangemaakt en verloopt na 15 min inactiviteit.

### (OPTIONEEL)
#### Must Have
* Als gebruiker wil ik mijn wachtwoord kunnen herstellen zodat ik weer kan inloggen.
  * Acceptatie: 'Wachtwoord vergeten' flow met beveiligde e-mail resetlink.
  * Acceptatie: resetlink verloopt na bepaalde tijd.

---

## Activiteit: Gebruik (auteur en lezer)
#### MVP
* Als auteur wil ik berichten (artikels/media) kunnen posten zodat ik content publiceer.
  * Acceptatie: nieuw bericht maken, titel/body, media upload; bericht zichtbaar na posten.
  * Acceptatie: media wordt gevalideerd (type/size).

#### Must Have
* Als gebruiker wil ik andere gebruikers kunnen volgen zodat ik hun posts in mijn feed zie.
  * Acceptatie: follow/unfollow werkt; feed-filter toont gevolgd materiaal.
* Als gebruiker wil ik kunnen zoeken zodat ik relevante posts of gebruikers vind.
  * Acceptatie: zoekresultaten zijn relevant en snel; beveiligd tegen injectie.
* Als auteur wil ik posts van mezelf en comments onder mijn posts kunnen verwijderen.
  * Acceptatie: verwijderactie bevestiging en correcte update.
* Als gebruiker wil ik mijn profiel kunnen aanpassen zodat mijn gegevens up-to-date zijn.
  * Acceptatie: profielvelden bewerkbaar, wijziging opgeslagen; re-authenticatie vereist bij wijzigen e-mail/wachtwoord.

---

## Activiteit: Uploaden
### Uploaden (schrijver)
#### MVP
* Als auteur wil ik media (afbeelding/video) bij een post kunnen uploaden zodat mijn content visueel wordt.
  * Acceptatie: media uploaden met grootte/format validatie; media gekoppeld aan post.
  * Acceptatie: geoptimaliseerde opslag.

#### Must Have
* Als auteur wil ik, wanneer ik dit wens, een leeftijdsverificatie instellen op mijn content zodat expliciete content enkel zichtbaar is voor toegestane gebruikers.
  * Acceptatie: content wordt afgeschermd waar nodig.

#### Nice to Have
* Als administrator wil ik spam kunnen voorkomen zodat het platform niet belaagd wordt met ongewenste content (bijv. via rate limiting).
* Als gebruiker wil ik andere gebruikers kunnen blokkeren zodat ik hun content niet meer zie.
* Als auteur wil ik drafts/concepten kunnen maken zodat ik op verschillende tijden kan werken aan posts.

---

## Activiteit: Commentaren en liken
#### MVP
* Als lezer wil ik comments kunnen plaatsen.
* Als lezer wil ik posts liken zodat ik waardering kan tonen.
  * Acceptatie: like-knop werkt en telt likes.
  * Acceptatie: comments worden opgeslagen en getoond; output wordt gesaneerd tegen XSS.

---

## Activiteit: Beveiliging
#### MVP
* Als systeem wil ik wachtwoorden veilig opslaan zodat gebruikersaccounts beschermd zijn.
  * Acceptatie: wachtwoorden gehasht (salted) opgeslagen; veilige resetflow.

#### Must Have
* Als moderator / systeem wil ik posts en comments kunnen verwijderen indien nodig.
  * Acceptatie: verwijderactie wordt gelogd in het audit-traject.

#### Nice to Have
* Als moderator / systeem wil ik kunnen modereren welke teksten op het platform staan.
  * Acceptatie: moderatie-interface beschikbaar voor de Administrator-rol.

---

## Activiteit: Opslag
#### MVP
* Als systeem moet ik basisaccountgegevens opslaan (e-mail, gebruikersnaam, versleuteld wachtwoord).
  * Acceptatie: velden aanwezig in DB-schema; beveiligde/versleutelde opslag in rust.

#### Must Have
* Als moderator / systeem moet ik de leeftijd van gebruikers kunnen verifiëren.
  * Acceptatie: leeftijdsveld en verificatieproces aanwezig conform privacy-richtlijnen.

#### Nice to Have
* Als moderator / systeem moet ik het aantal likes en comments kunnen zien per post.
  * Acceptatie: statistieken beschikbaar in de admin-omgeving.