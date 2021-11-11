## More quests

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
Add more NPCs with different quests and rewards. You can choose from different quest types.  
</div>
<div>
Image, gif or video showing what they will achieve by the end of the step. ![](images/image.png){:width="300px"}
</div>
</div>

--- task ---
Design your second quest. 

It could be:
+ A **gather** quest with multiple items of the same 

--- /task ---

For each quest you will need to:
+ Add a new NPC to be the quest giver. 
+ Update the QuestSeeker script on the Player with variables to store the state of the new quest. 
+ Add items and other NPCs depending on the quest type. 
+ Add a script to to the quest giver NPC and give it a name such as 'QuestGiver2'. Add a UI TextMeshPro message a UI TextMeshPro Button to the new quest giver. Add code to the script to control the conversation and reward based on the state of the quest.

+ Add scripts to items and other NPCs according to the quest type.

--- task ---

Add a new GameObject to be the second QuestGiver NPC. 

**Choose:**

--- collapse ---

---
title: Duplicate your first NPC and make changes to it
---

Right-click on the QuestGiver GameObject you created for the first quest and select 'Duplicate'. This creates a copy of your QuestGiver GameObject with all the child GameObjects. 

The QuestGiver GameObject will be created in the same position, use the Scene view or Inspector to position it somewhere else. 

Remove the existing 'QuestGiver' script component from the Inspector by clicking on the three dots and selecting 'Remove Component'.

--- /collapse ---

--- collapse ---

---
title: Add a new QuestGiver NPC GameObject
---

Choose a model or create a new QuestGiver NPC GameObject out of 3D shapes.  

Add a Box Collider so that the Player cannot walk through the new QuestGiver NPC and a second Box Collider, that is bigger than the first, with 'Is Trigger' checked. 

Right-click on the Canvas for your first NPC and choose copy. Then, right-click on your new QuestGiver NPC and choose 'Paste as Child'. 

--- /collapse ---

In the Inspector:
+ Edit the text in the Message on your new QuestGiver NPC Canvas to describe your new quest. Change the text style to suit your new character. 
+ Edit the text in the Name object to match your new NPC.


--- collapse ---

---
title: Create a new script for the QuestGiver NPC.
---

Create a new script for the QuestGiver NPC. The script will need a unique name such as QuestGiver2 or KeyQuestGiver. 

This script will control the initial state of collectables, the canvas messages and button, and the accepting of the task: 

```
using TMPro;

public class QuestGiver : MonoBehaviour
{
    public GameObject canvas;
    public GameObject button;
    public TMP_Text message
    public QuestSeeker player;

    // Start is called before the first frame update
    void Start()
    {
        Debug.Log("Quest giver start");
        canvas.SetActive(false);

        // Set up the quest
       
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            // Check quest condition and take action
            if (false) // Check the condition for your quest
            {
                message.SetText("Thankyou for completing the quest"); // add your message
                
                // Reward and result actions
                // Make sure reward can't be claimed again
            }

            canvas.SetActive(true);
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.SetActive(false);
        }
    }

    public void QuestAccepted()
    {
        Debug.Log("Quest accepted"); // Update with the name of your quest
        // Activate the quest

        canvas.SetActive(false);
        button.SetActive(false);
    }
}
```

--- /collapse ---

In the Inspector, making sure you are updating the child objects and components for your new QuestGiver NPC:
+ Drag the Canvas, Message and Button objects to your new Script,
+ Select the Button and add an 'OnClick' set to the `QuestAccepted` Method of your new script.

--- /task ---

--- task ---

**Test:** Play your scene and make sure you see the new quest message and that you can Accept the quest with the button. Check that you can see the debug message in the Console.

--- /task ---

--- task ---

Depending on the type of quest you have chosen, add or create the GameObjects that you will use as collectibles, followers or rewards and position them in your scene. 

Create a tag for your new GameObjects and apply the tag to them.

Add a Box Collider component to your item GameObject and check the 'Is Trigger' Box Collider property.

**Choose:** Add visual effects to your collectibles, followers or rewards.

--- collapse ---

---
title: Add a particle system to attract attention
---



--- /collapse ---

--- collapse ---

---
title: Add a ItemController script to spin your items
---

Upgrade the looks of the Item by creating an 'ItemController' script to code visual effects like spinning:

```
    public float spinSpeed = 5.0f; /

    // Update is called once per frame
    void Update()
    {
        transform.Rotate(Vector3.forward * spinSpeed); //you can also spin backward, up, down, left and right
    }

```

Remember to drag the 'ItemController' script to the Item GameObject

--- /collapse ---

--- collapse ---

---
title: Use animation to bring your items to life
---



--- /collapse ---

**Tip:** If all of your collectibles, followers or rewards are to look and act in the same way, make sure you add all your effects before duplicating the first GameObject. 

--- /task ---


--- task ---

--- collapse ---

---
title: Recipe or craft quest
---

In a recipe or craft quest, the player will need to collect multiple items of different kinds to make a recipe or craft a new item. 

Update the **QuestSeeker** script used by the player with variables to keep track of the items that have been collected:

```
// Add a variable for each item to be collected
public bool hasIceBlock = false;
public bool hasIceTool = false;
```

Add a script to each collectible item, so that it disappears and updates the QuestSeeker 
You will need to drag the Player GameObject in the inspector. 

Here's an example for an IceBlock, the same project also has a IceTool collectible GameObject with a similar script. 

```
public class IceBlockController : MonoBehaviour
{
    public QuestSeeker player;

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            player.hasIceBlock = true;
            Destroy(gameObject);
        }
    }
}

```

Update the new  QuestGiver NPC, the script will need a unique name, to handle the quest:

<mark>Highlight code to clearly show new elements</mark>
```
using TMPro;

public class QuestGiver2 : MonoBehaviour
{
    public GameObject canvas;
    public GameObject button;
    public GameObject iceBlock;
    public GameObject iceTool;
    public GameObject iceDome;
    public TMP_Text message;
    public QuestSeeker player;

    void Start()
    {
        // Don't show the quest message at the start
        canvas.SetActive(false);

        // Hide the quest items and reward or result objects
        iceBlock.SetActive(false);
        iceTool.SetActive(false);
        iceDome.SetActive(false);
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            // And && condition to check whether 
            if (player.hasIceBlock && player.hasIceTool)
            {
                // Change to a successful completion message
                message.SetText("Thankyou for helping me finish my ice dome. You can climb it if you like.");

                // Reward and story actions
                iceDome.SetActive(true);
                player.coins+= 20;

                // Make sure the reward can't be given again
                player.hasIceBlock = false;
                player.hasIceTool = false;
            }

            canvas.SetActive(true);
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            // Hide the message
            canvas.SetActive(false);
        }
    }

    public void QuestAccepted()
    {
        // Items to collect should appear. 
        iceBlock.SetActive(true);
        iceTool.SetActive(true);
        canvas.SetActive(false);
        button.SetActive(false);
    }
}

```

--- /collapse ---

--- collapse ---

---
title: Gather quest
---

In a 'Gather quest' the player will collect multiple items of the same type. 



Update your 'QuestSeeker' script to keep track of the number of collectables:

```
public int collectables = 0;
```

Add code to your 'CollectableController' script to destroy the Collectable GameObject and add one to the 'collectables' variable. 

You might also want to:
+ add to the total you displayed in quest one 
+ add a sound effect  

```
public QuestSeeker player;
public AudioClip collectSound;

void OnTriggerEnter(Collider other)
    {
    // Check the tag of the colliding object
        if (other.gameObject.tag == "Player")
        {
            Destroy(gameObject);
            player.collectables += 1;
            player.coins += 1; // overall score
            AudioSource.PlayClipAtPoint(collectSound, transform.position);

        }
    }
```

Drag the Player GameObject into the 'Player' property of the Collectable's 'CollectableController' script the Inspector window. 





```
using TMPro;

public class CollectableGiver : MonoBehaviour
{
    public GameObject canvas;
    public TMP_Text message;
    public GameObject button;
    public QuestSeeker player;
    GameObject[] collectables;

    // Start is called before the first frame update
    void Start()
    {
        canvas.SetActive(false);

        collectables = GameObject.FindGameObjectsWithTag("Collectable");
        foreach (var Collectable in collectables)
        {
            Collectable.SetActive(false);
        }
    }

    private void Update()
    {

    }

    public void CoinsAccepted()
    {
        foreach (var Collectable in collectables)
        {
            Collectable.SetActive(true);
        }

        canvas.SetActive(false);
        button.SetActive(false); // Don't show the Accept button again
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.SetActive(true);

            if (player.coins > 2) // if all the coins have been collected
            {
                message.SetText("Well done you collected the coins!");
              
            }

        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.SetActive(false);
        }
    }
```

--- /collapse ---

--- collapse ---

---
title: Deliver quest
---

Quest giver gives you an object to deliver to another NPC. Get a reward when you return.

--- /collapse ---

--- collapse ---

---
title: Escort quest
---

Find another NPC and escort them. This could be back to the Quest Giver NPC or to another NPC or GameObject. 

--- /collapse ---

--- collapse ---

---
title: Storytelling quest
---

Find out information from another NPC.

--- /collapse ---

--- collapse ---

---
title: Puzzle or task quest
---

Solve a puzzle. 

--- /collapse ---

--- /task ---

--- task ---

Choose a reward type. 

--- collapse ---

---
title: Coins or experience
---



--- /collapse ---

--- collapse ---

---
title: An accessory or follower
---



--- /collapse ---

--- collapse ---

---
title: Unlock
---

Remove a barrier or get access to an area or items that were not available previously. 

--- /collapse ---


--- /task ---

--- task ---

**Debug:** You might find some bugs in your project that you need to fix. Here are some common bugs.

--- collapse ---

---
title: Each debug in a collapse or ingredient
---

Each debug in a collapse or ingredient

--- /collapse ---

--- /task ---

--- save ---
