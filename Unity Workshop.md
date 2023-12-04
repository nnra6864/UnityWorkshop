[GitHub](https://www.github.com/nnra6864)
[Itch](https://nnra.itch.io/)
[Discord](_nnra/.nnra)
[Presentation on GitHub](https://www.github.com/nnra6864/UnityWorkshop)
# C# Basics
## Variables/Fields/Properties
### Variable
- **Pointer** to a place in memory where the **data** is stored
- Can be of various types such as **int**, **float**, **bool**, **string** etc.
### Field
- **Global variable**
- Can have **modifiers** such as **private**, **public**, **static** etc.
### Property
- **Field** with a **getter** and/or a **setter**
## Functions/Methods
### Function/Method
- Set of commands that the computer will execute when the function is called
- Can define **parameters** and accept **arguments**
- Can have a return type such as **int**, **string** etc.
### Method
- **Function** tied to a **class**
- Can have **modifiers** such as **private**, **public**, **static** etc.
- **C#** doesn't support functions independent of classes so everything is a **Method**
## Parameters/Arguments
### Parameter
- **Placeholder** for a **value** that'll be passed
- Has to have an **explicit type**
- Can be an **optional parameter** but has to be defined after all the **required parameters**
- Can be an **array** of a **specific type** but **unspecified length**, is defined with a keyword **params** and must come after all the **required** and **optional parameters**
### Argument
- **Value** passed to a **function** in the place of a **parameter**
- Has to match the **type** of the parameter
## Flow Statements
- Used to control the **flow** of the program
- Some of the most used statements are **if**, **else**, **while**, **switch**, **for** and **foreach**
## Class
- Wrapper for **functions**, **fields** and **properties**
- Can be **static**, **private**, **public**, **protected** and/or **internal**
- Can create an **object** from it if the class is not **static**
- Can inherit only one **base** or **derived** class but multiple interfaces
## Struct
- Almost the same as a **class** with the major difference being that it's passed by **value** and not the **reference**
## Constructor
- Initialization method for a **class** or a **struct**
- Is defined by appending **()** to the end of the **class**/**struct** name inside of the said **class**/**struct**
- All the **classes** and **structs** have a default **constructor**
- **Struct constructor** has to have **at least 1 parameter** and initialize all the fields
## Interface
- Blueprint that a **class** can inherit and has to implement all of it's **members**
## Static
- **Static** means that there can't be an instance of the said **class** or **variable**
## Namespace
- Wrapper for **classes**, **interfaces**, **structs** etc.
## Singleton
- A class with **only 1 instance** of itself
## Singleton Example
```cs
using UnityEngine;  
  
namespace Core  
{  
    public class GameManager : MonoBehaviour  
    {  
        private static GameManager _instance;  
        public static GameManager Instance  
        {  
            get => _instance;  
            set  
            {  
                if (Instance == value) return;  
                if (Instance != null)  
                {
                    Destroy(value.gameObject);  
                    return;  
                }
                _instance = value;  
                DontDestroyOnLoad(_instance);  
            }
        }
        private void Awake() => Instance = this;  
    }
}
```
## ref Keyword
- Used for getting/passing a **reference** from/to something.
# Unity Basics
## General
- **Unity** is based on a **component** system which means that every **object** in the **scene** has **components** that describe it's behavior
- **Unity** is both a **2D** and a **3D** engine
- **Unity** uses **C#** as it's main programming language but is written in **C++**
- Common misconception is that **Unity** can't have nice visuals and it came from a fact that it's easy to learn and most beginners use it which resulted in a ton of games that don't have decent looking assets
- Use name
## Windows
- **Scene View** displays all the **objects** currently present in the **scene**
- **Game View** displays the **current camera** and it's a place in which you'll do all the in-engine playtesting
- **Hierarchy** is a list of all the **objects** in the **current scene**
- **Inspector** displays all the **info** and **components** attached to a selected **game object/s**
- **Project** displays all the **folders** and **files** in your **project**
- **Console** displays all the **debug** info
- **Package Manager** is a window in which you'll manage all the **project packages**
## Buttons
- **Play** starts the game in the **current scene**
- **Pause** stops the **playback** of the game
- **Step** is used to jump to the **next frame**
- **Toggle Gizmos** toggles all the **gizmos** in the **scene view**
- **Orientation** displays the **current view orientation** and can be used to snap the view to a certain **axis**
- **Perspective/Isometric** is used to toggle between the view modes
## Project
### Setup
- Make sure that the **Event System** is present in the **scene** to avoid any potential **bugs**
- Create a **Plane** and scale it to the desired size(use the link feature to scale proportionally)
- Add a **Capsule**, rename it to **Player** and move it to a desired location
- **Parent** the **Main Camera** to the **Player** and adjust it's position
- Add a new **layer** called **Player**
- Change the **tag** and **layer** to **Player**
- Attach a **Rigidbody** to your **Player**
- Set the **Interpolate** to **Interpolate**
- Set the **Collision Detection** to **Continuous** in order to avoid any possible bugs related to **collision**
- Under the **Constraints** menu, enable the **Free Rotation** option for **X** and **Z axes**
### Movement and Game Manager
- Add a **Scripts** folder as well a **Player** subfolder
- Create a new **C# Script** and name it **PlayerMovement**
- Open the **PlayerMovement** script in an **IDE** of your choice
- Move the **class** to a correct **namespace**
- Delete all the code inside of the **class**
- To **move** the **player**, we have to change the attached **Rigidbody's velocity** and to do so, we need a **reference** to the **Rigidbody**
- Create a new **private Rigidbody field** in your **class** and name it **\_rb** `private Rigidbody _rb`
- In order to **serialize** it(expose it to the inspector), we'll use a **SerializeField attribute** `[SerializeField] private Rigidbody _rb`
- To avoid manually dragging the **Rigidbody** in the inspector, add a **Reset** function and write `_rb = GetComponent<Rigidbody>();`
- To ensure that the **Rigidbody** is attached to the **Player** we'll add a **RequireComponent** attribute to our **class**
- Add a new line above the **class** and write `[RequireComponent(typeof(Rigidbody))]`
- Inside of the **class**, add an **Update** function and write the following code in order to **get** and **debug** the **direction** of the **input**:
```cs
private void Update()
{
    Vector3 dir = new();
    dir.x = Input.GetAxisRaw("Horizontal");
    dir.z = Input.GetAxisRaw("Vertical");
    Debug.Log(dir);
}
```
 
- Attach the **PlayerMovement** script to the **Player**
- Test if the **console** is logging proper values based on your **input**
- Replace the **debug** line `dir.Normalize();` in order to **normalize** the direction(make it have a total value of 1)
- Create a new **private float field**, name it **\_speed and serialize it** `private float _speed;`
- **Serialize** this field `[SerializeField] private float _speed;`
- Create a new variable called **velocityDelta** in the **update** function and assign `dir * _speed` to it `var velocityDelta = dir * _speed;` after **normalizing** the dir
- Set your **Rigidbody's velocity** to this value `_rb.velocity = velocityDelta;`
- Set the **speed** in the inspector to 5 and test the movement out
- The last thing we have to implement in the **PlayerMovement** script is the **rotation**
- This can be done by calculating the **delta** of the **current** and **previous mouse positions**
- Since we'll also need the **delta mouse position** in the camera script, lets create a new **script** under the **Core** folder and call it **GameManager**
- Create a new **object** in the **scene**, call it **GameManager** and attach our newly created **script** to it
- Empty the **class** and move it to the proper **namespace**
- Make this **class** a **singleton** by following the [[#Singleton Example|example]]
- We can calculate the **mouse position delta** by **storing** the **previous mouse position** in a **private Vector3 field**, which we'll call **\_prevMousePos**, and **subtracting** it from the **current mouse position**
- To make the **delta field** visible to other **scripts**, we'll create a **getter** for it
- This is the code that does it:
```cs
private Vector3 _prevMousePos;
public static Vector3 MouseDelta { get; private set; }

private void Update()
{
    var mp = Input.mousePosition;
    _mouseDelta = mp - _prevMousePos;
    _prevMousePos = mp;
}
```
- Now that we have a **delta position** of our **mouse**, lets get back to implementing the **player rotation**
- If we try to **rotate** the Player in the **scene view**, we'll notice that the **X axis** is **UP/DOWN** while **Y axis** is **LEFT/RIGHT**
- That means that we have to **rotate** the **Player** on the **Y axis** for the value of the **X axis of the MouseDelta**
- In the **Update function** of our **PlayerMovement** script, we can achieve this by creating a new variable **rotDelta** that is a **Vector3** and doing `Vector3 rotDelta = new(0, GameManager.MouseDelta.x);`
- Then simply **rotate** our **player** for the **rotDelta** `transform.Rotate(rotDelta);`
- This is how the **PlayerScript** should look like now:
```cs
using Core;  
using UnityEngine;  
  
namespace Player  
{  
    [RequireComponent(typeof(Rigidbody))]  
    public class PlayerMovement : MonoBehaviour  
    {  
        [SerializeField] private Rigidbody _rb;  
        [SerializeField] private float _speed;  
        private void Reset()  
        {
            _rb = GetComponent<Rigidbody>();  
        }  
        private void Update()  
        {
            Vector3 dir = new();  
            dir.x = Input.GetAxisRaw("Horizontal");  
            dir.z = Input.GetAxisRaw("Vertical");  
            dir.Normalize();  
            var velocityDelta = dir * _speed;  
            _rb.velocity = velocityDelta;  
            var rotDelta = new Vector3(0, GameManager.MouseDelta.x);  
            transform.Rotate(rotDelta);  
        }
    }
}
```
### Camera
- You've probably noticed that our current implementation is missing the **UP/DOWN** movement so lets implement that
- Create a new **script** under the **Player** folder and call it **CameraMovement**
- Attach this **script** to the **Camera object**
- Empty the **class** and move it to the proper **namespace**
- Create a **private Camera field** and call it **\_cam** `private Camera _cam`
- To get a reference to the **camera**, we'll use the `Camera.main` inside of the **Awake** function `private void Awake() => _cam = Camera.main;`
- Go to the **scene view** and try rotating the camera on the X axis
- You'll notice that it's **inverted**
- That means that we have to negate the **Y axis** of the **MouseDelta** and assign it to the **X axis** of our **rotDelta**, which we'll achieve by doing `var rotDelta = new Vector3(-GameManager.MouseDelta.y, 0);`
- We can now **rotate** our **camera** by doing `_cam.transform.Rotate(rotDelta)`
### Polishing
- You may have noticed that the **sensitivity** is too fast and that we can **rotate** the **camera** without any **limits** so lets fix that
- Lets address the **sensitivity** issue first
- In our **GameManager**, add a new **serialized float** and call it **\_sensitivity** `[SerializeField] private float _sensitivity;`
- To make it **accessible** from other **scripts**, make a **static property** that gets the **\_sensitivity** from the **GameManager Instance** `public static float Sensitivity => Instance._sensitivity;`
- Navigate to your **PlayerMovement script** and multiply the value we are assigning to **rotDelta** by the **GameManager.Sensitivity** `var rotDelta = new Vector3(0, GameManager.MouseDelta.x) * GameManager.Sensitivity;`
- Do the same in the **CameraMovement script** `var rotDelta = new Vector3(-GameManager.MouseDelta.y, 0) * GameManager.Sensitivity;`
- Set the **Sensitivity** to something like **0.25** on your **GameManager object** and test it out
- Lets fix the **unlimited camera rotation** now
- To achieve this, we'll have to introduce a new **float field** and call it **\_totalRotation** `private float _totalRotation;`
- Purpose of this **variable** is to store the **current X rotation** of our camera
- Remove the `_cam.transform.Rotate(rotDelta)` line
- We should now add our **rotDelta.x** to the current **\_totalRotation** which can be achieved by doing `_totalRotation += rotDelta.x;`
- In order to limit the **min** and **max** values, we can utilize a **method** from the **Mathf** library called **Clamp** `_totalRotation = Mathf.Clamp(_totalRotation, -90, 90);`
- Assign **\_totalRotation** to **camera's local rotation** and that should take care of the issue we encountered `_cam.transform.localRotation = Quaternion.Euler(new(_totalRotation, 0));`
# Tips
- Keep the **project structure** clean and organized
- Use **namespaces**
- Try to figure out **logical problems** on your own but consult [documentation](https://docs.unity3d.com/ScriptReference/) and experienced people if you are **unfamiliar** with the **concept**
- Watch **devlogs** and other **game development** related **content**
- Get a firm understanding of **C#**
- Whenever you see something, try thinking of a way you'd **implement** it **in a game**
- **Don't rely** on **GPT** when it comes to **writing code** but absolutely ask it about the **concept** or even **how your code can be improved**
- Follow the **C#** [naming conventions](https://github.com/ktaranov/naming-convention/blob/master/C%23%20Coding%20Standards%20and%20Naming%20Conventions.md)
- Ask people for **feedback** and prompt them with **targeted questions**
# Scripts
## GameManager
```cs
using UnityEngine;

namespace Core
{
    public class GameManager : MonoBehaviour
    {
        private static GameManager _instance;
        public static GameManager Instance
        {
            get => _instance;
            set
            {
                if (Instance == value) return;
                if (Instance != null)
                {
                    Destroy(value.gameObject);
                    return;
                }
                _instance = value;
                DontDestroyOnLoad(_instance);
            }
        }
        private void Awake() => Instance = this;
        
        [SerializeField] private float _sensitivity;
        public static float Sensitivity => Instance._sensitivity;
        private Vector3 _prevMousePos;
        public static Vector3 MouseDelta { get; private set; }
        private void Update()
        {
            var mp = Input.mousePosition;
            MouseDelta = mp - _prevMousePos;
            _prevMousePos = mp;
        }
    }
}
```
## PlayerMovement
```cs
using Core;
using UnityEngine;

namespace Player
{
    [RequireComponent(typeof(Rigidbody))]
    public class PlayerMovement : MonoBehaviour
    {
        [SerializeField] private Rigidbody _rb;
        [SerializeField] private float _speed;
        private void Reset()
        {
            _rb = GetComponent<Rigidbody>();
        }
        private void Update()
        {
            Vector3 dir = new();
            dir.x = Input.GetAxisRaw("Horizontal");
            dir.z = Input.GetAxisRaw("Vertical");
            dir.Normalize();
            var velocityDelta = dir * _speed;
            _rb.velocity = velocityDelta;
            var rotDelta = new Vector3(0, GameManager.MouseDelta.x) * GameManager.Sensitivity;
            transform.Rotate(rotDelta);
        }
    }
}
```
## CameraMovement
```cs
using Core;
using UnityEngine;

namespace Player
{
    public class CameraMovement : MonoBehaviour
    {
        private Camera _cam;
        private Vector3 _prevMousePos;
        private float _totalRotation;
        private void Awake() => _cam = Camera.main;
        
        private void Update()
        {
            var rotDelta = new Vector3(-GameManager.MouseDelta.y, 0) * GameManager.Sensitivity;
            _totalRotation += rotDelta.x;
            _totalRotation = Mathf.Clamp(_totalRotation, -90, 90);
            _cam.transform.localRotation = Quaternion.Euler(new(_totalRotation, 0));
        }
    }
}
```