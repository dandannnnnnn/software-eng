flowchart RL
    B["Nieuwe Post Aanmaken"] --> n3["Tekst kiezen voor artikel"]
    n3 --> n2["Media invoegen"]
    A(["Inloggen in Account"]) --> n4["Profiel bekijken"]
    n4 --> n5["Heb ik al artikels geplaatst?"]
    n5 -- Nee --> B
    n5 -- Ja --> n6["Wil ik een bestaande post bewerken of verwijderen?"]
    n6 -- Verwijderen --> n7["Druk op de verwijder knop bij de post"]
    n6 -- Bewerken --> n8["Druk op de knop bewerken bij de post"]
    n2 --> n9["Wil ik het artikel nu al plaatsen of later?"]
    n9 -- Nu plaatsen --> n1["Plaatsen"]
    n9 -- Later plaatsen --> n10["Sla de post op als draft"]
    n8 --> n11["Doe de nodige aanpassingen"]
    n11 --> n9
    n1 --> n4
    n7 --> n4
    n10 --> n4

    n3@{ shape: rect}
    n2@{ shape: rect}
    n4@{ shape: rect}
    n5@{ shape: diam}
    n6@{ shape: diam}
    n7@{ shape: rect}
    n8@{ shape: rect}
    n9@{ shape: diam}
    n1@{ shape: rect}
    n10@{ shape: rect}
    n11@{ shape: rect}