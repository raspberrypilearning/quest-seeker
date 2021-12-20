
--- question ---

---
legend: Question 2 of 3
---

A script on a Quest Giver NPC has the following method:

--- code ---
---
language: cs
filename: QuestGiver.cs
line_highlights: 9
---
    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            if (player.hasQuestItem)
            {
                message.SetText("Thank you so much!");
                player.coins += 15; // Give the reward

            }

            canvas.SetActive(true);
        }
    }
--- /code ---

The game has a bug that allows the player to keep collecting more coins by repeatedly colliding with the NPC after completing the quest. Which line of code could you add after giving the reward to fix this?

--- choices ---

- ( ) 
```
player.coins -= 15;
```

  --- feedback ---

  No, that would remove the reward every time it was given, including the first time. The player would never get the reward.

  --- /feedback ---

- (x) 
```
player.hasQuestItem = false;
```

  --- feedback ---

Yes that's correct. The Quest Giver NPC checks whether the Player has the quest item before giving the reward. Setting the `player.hasQuestItem` variable to false will mean that the reward code doesn't run next time the Player collides with the Quest Giver NPC. 

  --- /feedback ---

- ( ) 
```
message.SetText("Hey, I already gave you a reward");
```

  --- feedback ---

No. This would just change the message the player sees. It wouldn't change the reward they are given. 

  --- /feedback ---

--- /choices ---

--- /question ---

