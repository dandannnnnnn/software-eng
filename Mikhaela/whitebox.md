# Blogging Platform Blackbox tests
#### Gemaakt door: Mikhaela Balaga 1ES
#### Groep: Thibau Vranken, Branko Claes, Mikhaela Balaga

# Whitebox Testplan: User Module (Gebruikersbeheer)

Dit document beschrijft de technische tests gericht op de code-architectuur, database-validaties en API-logica van de User Module.

## 1. Unit & Integratie Tests (Data & Logic)
| Test ID | Component | Test Scenariio | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| WB-01 | Password Hashing | Registratie proces aanroepen | Wachtwoord wordt via Argon2/BCrypt gehasht opgeslagen (nooit in plain-text). |
| WB-02 | Input Validatie Regex | `validateEmail()` functie | Regex moet RFC 5322 compliant zijn en edge-cases (zoals `test@sub.domain.com`) afvangen. |
| WB-03 | Database Uniqueness | SQL/NoSQL Unique Constraint | Directe DB-insert met dubbele gebruikersnaam moet een `UniqueConstraintViolation` gooien. |

## 2. API Endpoints
| Test ID | Endpoint | Methode | Validatie |
|:--- |:--- |:--- |:--- |
| WB-04 | `/api/user/profile` | PATCH | Controleer of alleen de velden `bio` en `avatar` geüpdatet kunnen worden (geen ID of rol-injectie). |
| WB-05 | `/api/user/follow` | POST | Check of een gebruiker zichzelf niet kan volgen (`target_id != follower_id`). |
| WB-06 | `/api/user/age-verify` | GET | Controleer de berekeningslogica: `current_date - birth_date` moet rekening houden met schrikkeljaren. |

## 3. Database Relaties
| Test ID | Entiteit | Test Scenariio | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| WB-07 | Volg-tabel | Cascade Delete | Als een gebruiker wordt verwijderd, moeten alle records in de `followers` tabel met dat ID ook verdwijnen. |
| WB-08 | Blokkeer-logica | Query Filter | Controleer of de SQL query voor de feed een `LEFT JOIN` met de `blocks` tabel bevat om content te excluderen. |

## 4. Beveiliging & Autorisatie
| Test ID | Type | Omschrijving | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| WB-09 | JWT/Sessie | Profiel wijzigen zonder token | Server moet een `401 Unauthorized` teruggeven. |
| WB-10 | ID Manipulation | Wijzigen van profiel van gebruiker B met token van gebruiker A | Server moet een `403 Forbidden` teruggeven. |