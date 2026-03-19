# Blackbox Tests – Post Module

## Module

Contentbeheer (Post Module)

## Beschrijving

De Post Module laat gebruikers blogposts maken, bewerken, opslaan als draft en verwijderen.
Blackbox tests controleren of deze functionaliteiten correct werken op basis van input en verwachte output, zonder de interne implementatie te kennen.

---

# Testcases

## 1. Post aanmaken (Create Post)

| Test ID | Input                 | Actie                  | Verwachte Output                                    |
| ------- | --------------------- | ---------------------- | --------------------------------------------------- |
| TC-P1   | Geldige titel + tekst | Klik op "Publish Post" | Post wordt opgeslagen en verschijnt in de postlijst |
| TC-P2   | Lege titel            | Klik op "Publish Post" | Foutmelding: titel is verplicht                     |
| TC-P3   | Lege content          | Klik op "Publish Post" | Foutmelding: content is verplicht                   |
| TC-P4   | Zeer lange tekst      | Post publiceren        | Post wordt correct opgeslagen zonder crash          |

---

## 2. Post bewerken (Edit Post)

| Test ID | Input                    | Actie                  | Verwachte Output                              |
| ------- | ------------------------ | ---------------------- | --------------------------------------------- |
| TC-P5   | Bestaande post aanpassen | Klik op "Save Changes" | Post wordt bijgewerkt met nieuwe inhoud       |
| TC-P6   | Titel wijzigen           | Save                   | Nieuwe titel wordt weergegeven                |
| TC-P7   | Content verwijderen      | Save                   | Foutmelding of lege post volgens specificatie |

---

## 3. Post als Draft opslaan

| Test ID | Input            | Actie              | Verwachte Output                        |
| ------- | ---------------- | ------------------ | --------------------------------------- |
| TC-P8   | Titel + tekst    | Klik "Save Draft"  | Post wordt opgeslagen als draft         |
| TC-P9   | Draft openen     | Klik op draft post | Draft kan opnieuw bewerkt worden        |
| TC-P10  | Draft publiceren | Klik "Publish"     | Draft verandert naar gepubliceerde post |

---

## 4. Post verwijderen

| Test ID | Input              | Actie                 | Verwachte Output                   |
| ------- | ------------------ | --------------------- | ---------------------------------- |
| TC-P11  | Bestaande post     | Klik "Delete Post"    | Post wordt verwijderd uit de lijst |
| TC-P12  | Delete bevestiging | Klik "Confirm Delete" | Post is definitief verwijderd      |
| TC-P13  | Delete annuleren   | Klik "Cancel"         | Post blijft bestaan                |

---

## 5. Foutafhandeling

| Test ID | Input                  | Actie        | Verwachte Output             |
| ------- | ---------------------- | ------------ | ---------------------------- |
| TC-P14  | Ongeldige input        | Submit       | Systeem toont foutmelding    |
| TC-P15  | Server error simulatie | Post opslaan | Gebruiker krijgt foutmelding |

---

# Samenvatting

De blackbox tests controleren of de Post Module correct reageert op gebruikersinput bij het maken, bewerken, opslaan en verwijderen van blogposts. De tests focussen op functionaliteit en verwachte outputs volgens de specificaties van de applicatie.
