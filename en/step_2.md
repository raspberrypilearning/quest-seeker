## First quest

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
The first quest will be a **fetch quest** where an NPC asks the player to find an item and bring it back to them. When the player returns to the quest giver they will be rewarded with experience points (XP) or a reward in the currency of your game.
<div>
Image, gif or video showing what they will achieve by the end of the step. ![](images/image.png){:width="300px"}
</div>
</div>

--- task ---

This project builds on the project you made in the [World Builder](https://projects.raspberrypi.org/en/projects/world-builder) project. 

Open your project to use as the world, or map, where quests will take place. 

--- /task ---

--- task ---
Think of a quest that makes sense in the world you have built. 

You will need to choose:
+ An item to be fetched,
+ A non-player character,
+ A reward of experience points or currency (coins or gems) in your game.

--- /task ---

--- task ---

Add a GameObject for the item that the player will need to fetch. Position the item in your world so the player will need to move from their starting position to find it. 

**Choose:**

--- collapse ---

---
title: Create an item from a model
---

Navigate to the Model you want to use in the Project window. 

Drag the model to your scene and position it: 

![The Scene view with the clover model added.](images/clover-scene.png)

--- /collapse ---

--- collapse ---

---
title: Create an item from 3D shapes
---

Add a '3D Object' to your scene to represent the item and give the new GameObject a sensible name.  

Right-click your new 3D shape and add other 3D shapes from 'Create' -> '3D Object' as child game objects. The child objects will move with the first 3D shape GameObject. 

Bring your shapes to life by dragging Materials from the Project window to the shape in the Scene view. 

This helmet has a sphere with child GameObjects that are spheres, a capsule and a cylinder. The shapes have been renamed to the part of the helmet they represent and coloured with Materials. 

![The Hierarchy window showing the 3D shape child objects that make up the whole item.](images/helmet-objects.png)

![A 3D shape item in Scene view.](images/helmet.png)

--- /collapse ---

--- collapse ---

---
title: Tag your item
---

**Create a new tag.** Go to the ‘Tag’ property at the top of the Inspector window and ‘Add Tag’. Click on the ‘+’ and call the new tag ‘Item’. GameObjects with an ‘Item’ tag will be things to be fetched as part of this quest.

**Apply your new tag.** Click on your GameObject in the Hierarchy window and use the Tag dropdown box to select ‘Item’ from the list.

--- /collapse ---

--- /task ---

--- task ---

Add a non-player character to be a Quest Giver. 

You could:
+ use one of the animal characters 

![The Hierarchy window showing the Raccoon GameObject and child GameObjects.](images/model-character-objects.png)

![The scene view with Raccoon character wearing constructuon gear.](images/model-character.png)

+ create your own character from 3D objects. 

![The Hierarchy window breakdown showing GameObject and child GameObjects for the character.](images/quest-giver-shapes.png)

![A 3D character in Scene view created out of shapes and the Hierarchy window breakdown showing GameObject and child GameObjects for the character.](images/quest-giver.png)

Position your NPC so that it will be easy for the player to find them.

Customise your character by dragging 'Materials' onto the GameObjects in the Scene view. This example uses the Cat model with a white 'Snow' material instead of its usual material:

![The Game view showing the Cat model with a white 'Snow' material added.](images/snow-cat.png)

--- /task ---

--- task ---

Add a Box Collider to the Quest Giver so that the player can't walk through them.

--- /task ---

The Quest Giver will offer the player a quest when they get close enough.

--- task ---
Add a UI TextMeshPro to the Quest Seeker GameObject for the message offereing the quest. 

You can add another UI TextMeshPro to the same canvas with the name of the Quest Giver NPC if you like. 

--- /task ---

--- task ---
Use a Box Collider with a Trigger to make the quest message appear when the Player is nearby. 

--- collapse ---

---
title: Make a text message appear when the player is close enough
---

Add another Box Collider with the Trigger property checked. This Box Collider needs to be bigger than the first Box Collider so that the player can trigger the Quest Giver to display a text box.

Add a script called 'QuestGiver' to the QuestGiver GameObject. Add `OnTriggerEnter` and `OnTriggerExit` methods to show and hide the message canvas when the Player gets close and moves away. 

```
public class QuestGiver : MonoBehaviour
{
    public Canvas canvas;

    // Start is called before the first frame update
    void Start()
    {
        canvas.enabled = false;
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.enabled = true;
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.enabled = false;
        }
    }
}
```

Select the QuestGiver GameObject. In the Inspector, find the QuestGiver script component and drag the Canvas for the NPC to the Canvas property of the script. 

<mark>Or we could use GetComponent?</mark>

--- /collapse ---

--- /task ---

--- task ---
Add a UI TextMesh Pro Button to the same canvas and give it the text 'Accept'.

Add code to the QuestGiver script to control when the object appears so that it only appear when then quest has been accepted. 

--- collapse ---

---
title: Make a GameObject appear when a button is clicked
---

```
public class QuestGiver : MonoBehaviour
{
    public Canvas canvas;
    public GameObject item;

    // Start is called before the first frame update
    void Start()
    {
        canvas.enabled = false;
        item.SetActive(false);
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.enabled = true;
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.enabled = false;
        }
    }

    void QuestAccepted()
    {
        item.SetActive(true);
    }
}
```

--- /collapse ---

--- /task ---

--- task ---
Allow the player to collect the item.
--- /task ---

--- task ---
Have the quest giver NPC display a different message if the quest is complete. 
--- /task ---

--- task ---
Give the player a reward for completing the quest. 

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
