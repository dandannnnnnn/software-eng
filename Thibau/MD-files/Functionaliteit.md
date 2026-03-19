# Functionaliteit per Module


## 1. User Module (Gebruikersbeheer)
Deze module beheert de identiteit en de sociale relaties van de gebruiker op het platform.

| Functionaliteit | Beschrijving | Prioriteit |
| :--- | :--- | :--- |
| **Registratie** | Gebruikers kunnen een account aanmaken via e-mail, gebruikersnaam en wachtwoord met invoervalidatie. | MVP |
| **Profielbeheer** | Gebruikers kunnen hun eigen profielgegevens inzien en wijzigen om deze up-to-date te houden. | Must-Have |
| **Volg-systeem** | Functionaliteit om andere gebruikers te volgen of te ontvolgen. | Must-Have |
| **Leeftijdsverificatie** | Opslaan en verifiëren van de geboortedatum/leeftijd ten behoeve van content-restricties. | Must-Have |
| **Blokkeer-systeem** | Gebruikers kunnen anderen blokkeren om hun content te verbergen en interactie te stoppen. | Nice-to-Have |

## 2. Auth Module (Authenticatie & Beveiliging)
Verantwoordelijk voor de toegang tot het systeem en de bescherming van gebruikersgegevens.

| Functionaliteit | Beschrijving | Prioriteit |
| :--- | :--- | :--- |
| **Login Systeem** | Valideren van credentials en het veilig aanmaken van een gebruikerssessie. | MVP |
| **Wachtwoord Hashing** | Wachtwoorden worden nooit in plain-text opgeslagen, maar veilig gehasht. | MVP |
| **Input Sanitization** | Voorkomen van SQL-injection en XSS-aanvallen door alle gebruikersinput te cleansen. | MVP |
| **Wachtwoord Herstel** | Een 'wachtwoord vergeten' flow waarbij via e-mail een tijdelijke resetlink wordt verstuurd. | Must-Have |
| **GDRP** | Naleving van de General Data Protection Regulation. | MVP |
| **Date Encrypteren** | Gevoelig data mag nooit zonder encryptie verstuurd worden tegen onderschepping. | MVP |

## 3. Post Module (Contentbeheer)
De kernmodule voor het creëren en beheren van de blog-content.

| Functionaliteit | Beschrijving | Prioriteit |
| :--- | :--- | :--- |
| **Publiceren** | Aanmaken van posts met titel en tekstinhoud die direct zichtbaar zijn op het platform. | MVP |
| **Eigen Beheer** | Auteurs kunnen hun eigen posts en de comments onder hun posts verwijderen. | Must-Have |
| **Leeftijdsrestricties** | Instellen van een vlag op posts waardoor deze enkel voor 18+ gebruikers zichtbaar zijn. | Must-Have |
| **Drafts (Concepten)** | Het opslaan van niet-gepubliceerde posts om er later aan verder te werken. | Nice-to-Have |

## 4. Interaction Module (Interactie & Discovery)
Beheert de betrokkenheid van gebruikers en de vindbaarheid van content.

| Functionaliteit | Beschrijving | Prioriteit |
| :--- | :--- | :--- |
| **Likes & Comments** | Gebruikers kunnen waardering tonen via een like-knop en tekstuele reacties achterlaten. | MVP |
| **Zoekmachine** | Een efficiënte zoekfunctie om posts en andere gebruikers te vinden op basis van trefwoorden. | Must-Have |
| **Persoonlijke Feed** | Een overzicht van content die gefilterd is op basis van de gevolgde auteurs. | Must-Have |

## 5. Storage Module (Data & Media)
De technische laag die verantwoordelijk is voor de opslag en integriteit van gegevens.

| Functionaliteit | Beschrijving | Prioriteit |
| :--- | :--- | :--- |
| **Media Upload** | Uploaden van afbeeldingen en video's met strikte validatie op bestandstype en grootte. | MVP |
| **Database Schema** | Beheer van de relationele database (gebruikers, posts, interacties) en back-up mogelijkheden. | MVP |
| **Media Optimalisatie** | Automatisch schalen of comprimeren van geüploade media voor snellere laadtijden. | MVP |
| **Server-side Validatie** | Controle van alle data voordat deze definitief in de database wordt opgeslagen. | MVP |

## 6. Admin Module (Moderatie & Beheer)
Tools voor de administrator om de kwaliteit en veiligheid van het platform te waarborgen.

| Functionaliteit | Beschrijving | Prioriteit |
| :--- | :--- | :--- |
| **Content Moderatie** | Het verwijderen van ongewenste posts of comments (inclusief logging van deze acties). | Must-Have |
| **Spam Preventie** | Systeem- en handmatige tools om spammers en bots te blokkeren. | Nice-to-Have |
| **Moderatie Interface** | Een specifiek dashboard voor admins om teksten te beheren en te modereren. | Nice-to-Have |
| **Statistieken Dashboard** | Inzien van analytics zoals het aantal likes en reacties per post. | Nice-to-Have |

---