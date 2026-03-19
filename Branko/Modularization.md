#Modularization Herschrijving
###Groep: Thibault Vranken, Branko Claes, Mikhaela Balaga

##Moduleringsstrategie
Dit is een goede methode om een softwareproject aan te pakken en een goed resultaat te geven. 

Dit methode splitst grote problemen op in kleinere problemen of modules. Er wordt niet naar data gekeken maar naar wat het programma moet doen (functionaliteit). Hierbij wordt een SRS gebruikt zodat men hiervan een werkend en leverbaar project van kunnen maken.

Het principe van Separation of Concerns (SoC) wordt gebruikt. 

##Basisprincipes
1. Alles dat een verband heeft met elkaar en hetzelfde doel hebben, behoren tot ééndezelfde module. 

2. Modules moeten onafhankelijk zijn van elkaar. Als de ene module wordt aangepast dan mogen de andere modules niet kapot gaan. 

##Functionele Categorisering
Er zijn vier lagen die men gebruikt om meeste software op te splitsen. 

**1. Domein Module:**Dit bevat alle logica van de applicatie (berekeningen, data-verwerking, ...)

**2. Storage Module:**Verantwoordelijk voor het opslaan en ophalen van informatie.

**3.User Module:**Alle interactie met de buitenwereld (gebruikersinvoer, schermweergave, ...).

**4. Helper Module:**Herbruikbare logica die overal in het project gebruikt kunnen worden (logging, datum-formattering, ...).

##Stappenplan
###Stap 1: Analyseer de SRS
Het is best om eerst door de SRS te gaan en met groepsleden te bespreken welke acties de belangrijkste zijn. Dit doet men zonder te programmeren. 

Om het efficiënt aan te pakken is het best om alle werkwoorden te markeren (bv.: registreren, inloggen, ...) om de **functies** in kaart te brengen.

###Stap 2: Groeperen
Alle functies die in dezelfde groep horen moeten samen in een groep behoren. 

bijvoorbeeld:
**Opslag:**Alles met databases
**Beveiliging:** Alles met wachtwoorden opslaan en veilig bijhouden. 

Men gebruikt voor de groeperingen benamingen zoals Security Box, User Box, ...

Men moet ervoor zorgen dat 1 module over 1 bepaald groep (module) gaat en dat Beveiliging en Opslag niet samen in 1 groep zitten. Dit zorgt voor minder verwarring en meer werkefficiëntie.

###Stap 3: Functionaliteit Definiëren
Zodat andere developers of medecollega's de modules begrijpen moeten de functionaliteiten per modules gedefiniëerd worden. 

Per module moet het doel gedocumenteerd zijn. Het mag niet te gedetailleerd zijn, een algemene beschrijving is goed genoeg.

Bijvoorbeeld User module:
Deze module is verantwoordelijk voor het aanmaken van nieuwe gebruikersprofielen; gebruikersnaam aanpassen, bijwerken van bio op profiel, ...

###Stap 4: Data Flows
Data is zeer belangrijk zodat alles vloeiend werkt van het project. 

Hierbij moet men bepalen welke data moet aankomen (input) en welke data moet teruggestuurd worden (output)?

voorbeeld input: 
User module heeft gebruikersnaam en wachtwoord nodig van de gebruiker zodat deze module kan starten.

voorbeeld output: 
User module geeft een signaal door naar de interface om te laten weten of dataoverdracht succesvol of onsuccesvol is gebeurd.

###Stap 5: Software Development
Om al deze modules in een softwareproject om te zetten moet men voor elke module 

________________________________________________________________________________________________________________________________________________________________________________________________________
#Gemini Prompt
Dit is een universeel stappenplan dat je op elk softwareproject (vooral in C) kunt toepassen om van een eisenlijst (SRS) naar een technisch ontwerp te gaan.

---

### Methode: Functionele Decompositie (De "Top-Down" aanpak)
Bij deze methode hak je een groot, complex probleem in steeds kleinere stukjes (modules). Je kijkt niet naar de data, maar naar **wat het programma moet doen** (de functies).

---

### Het Stappenplan (Toepasbaar op elk project)

#### Stap 1: Analyseer de SRS op "Werkwoorden"
Lees je requirements en identificeer de belangrijkste acties.
*   *Voorbeeld:* "Inloggen", "Berekenen", "Opslaan", "Weergeven", "Verwijderen".
*   **Actie:** Maak een lijstje van alle unieke acties die je systeem moet uitvoeren.

#### Stap 2: Groepeer functies in Logische Modules
Kijk naar je lijst uit stap 1 en groepeer functies die bij elkaar horen. Een goede vuistregel voor modules is:
1.  **User/Auth:** Alles over wie de gebruiker is.
2.  **Core Logic:** De hoofdfunctie van je app (bijv. berekeningen of tekstverwerking).
3.  **Data/Storage:** Alles wat met de database of bestanden te maken heeft.
4.  **UI/Interface:** Alles wat de gebruiker ziet (menu's, schermen).
5.  **Admin/Tools:** Beheerfuncties en hulpfuncties.

#### Stap 3: Definieer de Modules (.md formaat)
Beschrijf voor elke module kort en krachtig wat het doel is.
*   *Vraag jezelf af:* "Als ik deze module weglaat, welk deel van mijn programma werkt dan niet meer?"

#### Stap 4: Beschrijf de Functionaliteit per Module
Maak een tabel of lijst met de specifieke taken. Gebruik actieve taal.
*   *Voorbeeld:* "Module X valideert input Y en geeft resultaat Z."

#### Stap 5: Breng de Data Flows in kaart (Input/Output)
Dit is de belangrijkste stap voor programmeurs. Je bepaalt hoe modules met elkaar praten.
*   **Input:** Welke informatie heeft de module nodig om zijn werk te doen?
*   **Output:** Wat levert de module op voor de volgende stap?
*   *Tip:* In C zijn dit vaak de parameters die je meegeeft aan een functie en de `return` waarde.

---

### Voorbeeld: Algemeen Framework (Template)

Als je dit moet invullen voor een willekeurig nieuw project, ziet de structuur er zo uit:

| Module Naam | Hoofdtaak | Voorbeeld Functionaliteit |
| :--- | :--- | :--- |
| **Interface Module** | Interactie met de gebruiker | Tonen van menu's, inlezen van toetsenbordinput. |
| **Logic Module** | Het "brein" van het programma | Berekeningen uitvoeren, regels controleren. |
| **Storage Module** | Geheugen/Opslag | Schrijven naar .txt of .db bestanden, inladen data. |
| **Security Module** | Toegang en veiligheid | Controleren van rechten, versleutelen van data. |

**Data Flow Schema (Algemeen):**
1.  **Input:** Gebruiker voert data in via **Interface**.
2.  **Verwerking:** **Interface** stuurt ruwe data naar **Logic**.
3.  **Check:** **Logic** vraagt **Security** of dit mag.
4.  **Opslag:** **Logic** stuurt het resultaat naar **Storage**.
5.  **Terugkoppeling:** **Storage** bevestigt succes aan **Interface** (om aan gebruiker te tonen).

---

### Waarom dit werkt voor C:
In C vertaal je dit direct naar je bestandsstructuur:
*   `user.h` / `user.c`
*   `logic.h` / `logic.c`
*   `storage.h` / `storage.c`

Door dit stappenplan te volgen, voorkom je dat je één enorme `main.c` krijgt ("Spaghetti code") en voldoe je aan de eisen van Software Engineering.