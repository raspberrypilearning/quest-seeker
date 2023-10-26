
--- question ---

---
legend: Question 2 sur 3
---

Un script sur un PNJ Donneur de quête a la méthode suivante :

--- code ---
---
language: cs
filename: QuestGiver.cs
line_highlights: 9
---

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Joeuer")
        {
            if (joeuer.aObjetQuete)
            {
                message.SetText("Merci beaucoup !");
                joeuer.pieces += 15; // Donner la récompense
    
            }
    
            canvas.SetActive(true);
        }
    }
--- /code ---

Le jeu comporte un bug qui permet au joueur de continuer à collecter plus de pièces en entrant en collision de façon répétée avec le PNJ après avoir terminé la quête. Quelle ligne de code pourrais-tu ajouter après avoir donné la récompense pour résoudre ce problème ?

--- choices ---

- ( )
```
joeuer.pieces -= 15;
```

  --- feedback ---

  Non, cela supprimerait la récompense à chaque fois qu'elle est donnée, y compris la première fois. Le joueur ne recevrait jamais la récompense.

  --- /feedback ---

- (x)
```
joeuer.aObjetQuete = false;
```

  --- feedback ---

Oui, c'est correct. Le PNJ Donneur de quête vérifie si le joueur possède l'objet de quête avant de lui donner la récompense. En définissant la variable `joeuer.aObjectquete` sur false, le code de récompense ne s'exécutera pas la prochaine fois que le joueur entrera en collision avec le PNJ Donneur de quête.

  --- /feedback ---

- ( )
```
message.SetText("Hé, je t'ai déjà donné une récompense.");
```

  --- feedback ---

Non. Cela changerait simplement le message que le joueur voit. Cela ne changerait rien à la récompense qui leur est accordée.

  --- /feedback ---

--- /choices ---

--- /question ---

