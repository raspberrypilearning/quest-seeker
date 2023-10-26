
--- question ---

---
legend: Vraag 2 van 3
---

Een script van een Queestegever NPC heeft de volgende methode:

--- code ---
---
language: cs
filename: QuestGiver.cs
line_highlights: 9
---

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Speler")
        {
            if (speler.heeftOpdrachtItem)
            {
                bericht.SetText("Heel erg bedankt!");
                speler.munten += 15; // Geef de beloning
    
            }
    
            canvas.SetActive(true);
        }
    }
--- /code ---

Het spel heeft een bug waarbij de speler meer munten kan blijven verzamelen door herhaaldelijk met de NPC te botsen nadat hij de zoektocht heeft voltooid. Welke regel code kun je toevoegen nadat je de beloning hebt gegeven om dit op te lossen?

--- choices ---

- ( )
```
speler.munten -= 15;
```

  --- feedback ---

  Nee, dat zou de beloning iedere keer verwijderen, inclusief de eerste keer. De speler zou de beloning nooit krijgen.

  --- /feedback ---

- (x)
```
player.hasQuestItem = false;
```

  --- feedback ---

Ja dat is goed. De Queestegever NPC controleert of de speler het gezochte item heeft voordat je de beloning geeft. De `speler.heeftOpdrahctItem` variabele op onwaar zetten betekent dat de volgende keer dat de speler botst met de Queestegever NPC de beloningscode niet wordt uitgevoerd.

  --- /feedback ---

- ( )
```
bericht.SetText("Hé, ik heb je al een beloning gegeven.");
```

  --- feedback ---

Nee. Dit zou alleen het bericht dat de speler ziet veranderen. Het zou de beloning die wordt gegeven niet veranderen.

  --- /feedback ---

--- /choices ---

--- /question ---

