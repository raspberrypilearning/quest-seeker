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
+ A **gather** quest with multiple items of the same kind.
+ A **recipe** or **crafting** quest with multiple items of different kinds. 
+ An **escort** quest where you have to find another NPC and have them follow the player back to the Quest Giver (or to another location)
+ A **deliver** quest where you are given an object to take to another NPC. 

The reward could be:
+ Experience points (XP), coins, gems or another in-game currency.
+ An accessory for the player. 
+ Unlocking an new area or item in the game. 

Or, a combination of these. 

Decide how you can avoid the Player completing the quest before they have completed it. You could:
+ Use `SetActive` to make the quest items appear when the quest is accepted.
+ Use a `questAccepted` variable to ignore the player if the quest has not been accepted. 

Or, you could allow the player to complete the request and get their reward immediately after accepting it. 

--- /task ---

For each quest you will need to:
+ Add a new NPC to be the quest giver with UI objects to communicate about the quest. 
+ Update the QuestSeeker script on the Player with variables to store the state of the new quest. 
+ Add items and other NPCs depending on the quest type. 
+ Add a script to to the quest giver NPC to control the conversation and reward based on the state of the quest.
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

This script will control the initial state of collectables, the canvas messages and button, and accepting the task: 

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

**Choose:** What happens when your Player gets a collectible, follower or reward? This will depend upon which type of quest you are creating:

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

A type of reward could be to remove a barrier or get access to an area or items that were not available previously. 

Think about the GameOjbects you want to remove. Create and apply a new 'Unlock' tag to them.

Create an unlock script and attach it to a new NPC quest ally or to a collectable item. 

```
public class Unlock : MonoBehaviour
{
    public GameObject canvas;
    public AudioClip collectSound;
    public CoinQuest walls;

    // Start is called before the first frame update
    void Start()
    {
       
        canvas.SetActive(false);
    }

    // Update is called once per frame
    void Update()
    {

    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
        
            canvas.SetActive(true);
            AudioSource.PlayClipAtPoint(collectSound, transform.position);

            foreach (var YellowWall in walls.walls)
            {
                YellowWall.SetActive(false);
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
}
```

--- /collapse ---


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

Update the new  QuestGiver NPC script:

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

Add code to your collectables controller script to destroy the collectable item GameObject and add one to the 'collectables' variable. 

You might also want to:
+ add to the total you displayed in quest 1 
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

Drag the Player GameObject into the 'Player' property of the Collectable's controller script the Inspector window. 

Add code to your Quest Giver NPC script create a new variable to store the  GameObjects that have a collectable/item tag and set their states at different points in the quest. Complete your OnTriggerEnter method to change the message only when all the items have been collected:

```
using TMPro;

public class QuestGiverNPC : MonoBehaviour
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

Make sure you have a QuestGiver NPC and a Follower NPC. 

Update the **QuestSeeker** script used by the player with variables to keep track of the quest:

```
    // The follower should only follow if the quest has been accepted
    public bool followQuestAccepted = false;

    // Set to true when the follower is following the player
    public bool friendFollower = false;
```

Add a script to the Follower NPC to get them to follow the player if the quest has been accepted but not completed. 
You will need to add a Box Collider with a Trigger. Make this bigger than other colliders on the NPC so that the following behaviour can be triggered but the player can't walk through or over the follower. 

If your follower NPC uses the 'IdleWalk' animator then you should also update the `isMoving` parameter to control the animation used.

```
public class FriendFollower : MonoBehaviour
{
    public QuestSeeker Player; 
    public float followSpeed = 3f;
    public float followDistance = 1.6f;
    Animator anim;

    // Start is called before the first frame update
    void Start()
    {
        anim = gameObject.GetComponent<Animator>();
        anim.SetBool("isMoving", false);
    }

    // Update is called once per frame
    void Update()
    {
        transform.LookAt(Player.transform);

        if(Player.friendFollower == true && Vector3.Distance(Player.transform.position, transform.position) > followDistance)
        {
                anim.SetBool("isMoving", true);
                CharacterController controller = GetComponent<CharacterController>();                
                var moveDirection = Vector3.Normalize(Player.transform.position - transform.position);
                controller.SimpleMove(moveDirection * followSpeed);           
        }
        else
        {
            anim.SetBool("isMoving", false);
        }       
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player" && Player.followQuestAccepted)
        {
            Player.hasFollower = true;
        }
    }
}

```

You will need to add a Box Collider (without a Trigger) around the Follower to make sure that the player can't climb on top of them!

Update the script you added to your QuestGiver NPC to set up the quest and give rewards. 

```
using TMPro;

public class EscortQuestGiver : MonoBehaviour
{
    public GameObject canvas;
    public GameObject button;
    public TMP_Text message;
    public HillQuestSeeker player;

    void Start()
    {
        Debug.Log("Escort quest start");
        // Don't show the quest message at the start
        canvas.SetActive(false);
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            if (player.friendFollower)
            {
                // Change to a successful completion message
                message.SetText("Thankyou finding my friend.");

                // Reward and story actions
                player.coins+= 20;
                player.friendFollower = false;
                player.followQuestAccepted = false;
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
        Debug.Log("Escort quest accepted");

        // Follower will now follow if player gets close
        player.followQuestAccepted = true;

        button.SetActive(false);  
        canvas.SetActive(false);     
    }
}

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
