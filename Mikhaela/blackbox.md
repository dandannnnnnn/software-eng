# Blogging Platform Blackbox tests
#### Gemaakt door: Mikhaela Balaga 1ES
#### Groep: Thibau Vranken, Branko Claes, Mikhaela Balaga

# Blackbox Testplan: User Module (Gebruikersbeheer)

Dit document beschrijft de functionele tests voor de User Module. De focus ligt op de input en de verwachte output voor de eindgebruiker.

## 1. Registratie
| Test ID | Omschrijving | Invoer | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| BB-01 | Succesvolle registratie | Geldig e-mail, gebruikersnaam en wachtwoord | Account wordt aangemaakt, gebruiker wordt ingelogd. |
| BB-02 | Registratie met ongeldig e-mail | E-mail zonder @ of domein | Foutmelding: "Ongeldig e-mailformaat". |
| BB-03 | Registratie met bestaande naam | Reeds geregistreerde gebruikersnaam | Foutmelding: "Gebruikersnaam is al bezet". |

## 2. Profielbeheer
| Test ID | Omschrijving | Actie | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| BB-04 | Wijzigen profielgegevens | Veranderen van biografie of profielfoto | Gegevens worden opgeslagen en getoond na verversen. |
| BB-05 | Profiel inzien | Navigeren naar eigen profiel | Alle huidige opgeslagen gegevens zijn zichtbaar. |

## 3. Volg-systeem
| Test ID | Omschrijving | Actie | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| BB-06 | Gebruiker volgen | Klik op 'Volgen' bij een andere gebruiker | Knop verandert in 'Volgend', teller volgers stijgt met 1. |
| BB-07 | Gebruiker ontvolgen | Klik op 'Ontvolgen' | Knop verandert terug naar 'Volgen', teller daalt met 1. |

## 4. Leeftijdsverificatie
| Test ID | Omschrijving | Actie | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| BB-08 | Minderjarige gebruiker | Geboortedatum instellen op < 18 jaar geleden | Content met restricties is niet zichtbaar/toegankelijk. |
| BB-09 | Meerderjarige gebruiker | Geboortedatum instellen op > 18 jaar geleden | Alle content is volledig toegankelijk. |

## 5. Blokkeer-systeem
| Test ID | Omschrijving | Actie | Verwacht Resultaat |
|:--- |:--- |:--- |:--- |
| BB-10 | Gebruiker blokkeren | Klik op 'Blokkeer' bij een andere gebruiker | Content van deze gebruiker verdwijnt uit de feed; interactie is onmogelijk. |