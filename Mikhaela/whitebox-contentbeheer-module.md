# Whitebox Tests – Post Module

## Beschrijving

Whitebox tests controleren de interne logica van de Post Module.
Hierbij wordt gekeken naar de codepaden, condities en functies binnen de module.
De tests verifiëren dat alle mogelijke codebranches correct uitgevoerd worden.

---

# Metacode van de Post Module

```pseudo
function createPost(title, content, status):

    if title is empty:
        return ERROR_TITLE_REQUIRED

    if content is empty:
        return ERROR_CONTENT_REQUIRED

    post = new Post(title, content, status)

    save post to database

    return SUCCESS
```

```pseudo
function editPost(postId, title, content):

    post = database.getPost(postId)

    if post does not exist:
        return ERROR_POST_NOT_FOUND

    post.title = title
    post.content = content

    update post in database

    return SUCCESS
```

```pseudo
function deletePost(postId):

    post = database.getPost(postId)

    if post does not exist:
        return ERROR_POST_NOT_FOUND

    remove post from database

    return SUCCESS
```

---

# Whitebox Testcases

## 1. createPost()

| Test ID | Codepad       | Beschrijving                               | Verwachte Resultaat    |
| ------- | ------------- | ------------------------------------------ | ---------------------- |
| WT-P1   | title check   | Titel is leeg                              | ERROR_TITLE_REQUIRED   |
| WT-P2   | content check | Content is leeg                            | ERROR_CONTENT_REQUIRED |
| WT-P3   | success path  | Geldige titel en content                   | SUCCESS                |
| WT-P4   | database save | Controle of save functie wordt aangeroepen | Post opgeslagen        |

---

## 2. editPost()

| Test ID | Codepad         | Beschrijving                    | Verwachte Resultaat  |
| ------- | --------------- | ------------------------------- | -------------------- |
| WT-P5   | post lookup     | Post bestaat niet               | ERROR_POST_NOT_FOUND |
| WT-P6   | update path     | Post bestaat en wordt aangepast | SUCCESS              |
| WT-P7   | database update | Update functie wordt uitgevoerd | Post gewijzigd       |

---

## 3. deletePost()

| Test ID | Codepad         | Beschrijving               | Verwachte Resultaat  |
| ------- | --------------- | -------------------------- | -------------------- |
| WT-P8   | post lookup     | Post bestaat niet          | ERROR_POST_NOT_FOUND |
| WT-P9   | delete path     | Post bestaat               | SUCCESS              |
| WT-P10  | database delete | Delete operatie uitgevoerd | Post verwijderd      |

---

# Samenvatting

De whitebox tests controleren de interne logica van de Post Module.
Alle belangrijke codepaden zoals validatie, database interactie en foutafhandeling worden getest om te verzekeren dat de implementatie correct werkt volgens de specificaties.
