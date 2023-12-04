[GitHub](https://www.github.com/nnra6864)
[Itch](https://nnra.itch.io/)
[Discord](_nnra/.nnra)

# C# Basics:
- ## Variables/Fields/Properties
	- ### Variable
		- **Pointer** to a place in memory where the **data** is stored
		- Can be of various types such as **int**, **float**, **bool**, **string** etc.
	- ### Field
		- **Global variable**
		- Can have **modifiers** such as **private**, **public**, **static** etc.
	- ### Property
		- **Field** with a **getter** and/or a **setter**
- ## Functions/Methods
	- ### Function/Method
		- Set of commands that the computer will execute when the function is called
		- Can define **parameters** and accept **arguments**
		- Can have a return type such as **int**, **string** etc.
	- ### Method
		- **Function** tied to a **class**
		- Can have **modifiers** such as **private**, **public**, **static** etc.
		- **C#** doesn't support functions independent of classes so everything is a **Method**
- ## Parameters/Arguments
	- ### Parameter
		- **Placeholder** for a **value** that'll be passed
		- Has to have an **explicit type**
		- Can be an **optional parameter** but has to be defined after all the **required parameters**
		- Can be an **array** of a **specific type** but **unspecified length**, is defined with a keyword **params** and must come after all the **required** and **optional parameters**
	- ### Argument
		- **Value** passed to a **function** in the place of a **parameter**
		- Has to match the **type** of the parameter
- ## Flow Statements
	- Used to control the **flow** of the program
	- Some of the most used statements are if, else, while, switch, for and foreach
- ## Class
	- Wrapper for **functions**, **fields** and **properties**
	- Can be **static**, **private**, **public**, **protected** and/or **internal**
	- Can create an **object** from it if the class is not **static**
	- Can inherit only one **base** or **derived** class but multiple interfaces
- ## Struct
	- Almost the same as a **class** with the major difference being that it's passed by **value** and not the **reference**
- ## Constructor
	- Initialization method for a **class** or a **struct**
	- Is defined by appending **()** to the end of the **class**/**struct** name inside of the said **class**/**struct**
	- All the **classes** and **structs** have a default **constructor**
	- **Struct constructor** has to have **at least 1 parameter** and initialize all the fields
- ## Interface
	- Blueprint that a **class** can inherit and has to implement all of it's **members**
- ## Static
	- **Static** means that there can't be an instance of the said **class** or **variable**
- ## Namespace
	- Wrapper for **classes**, **interfaces**, **structs** etc.
- ## Singletons
	- A class with **only 1 instance** of itself
- ## Example of a singleton:
```cs
private static Test _instance;
public static Test Instance
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
```
- ## ref Keyword
	- Used for getting/passing a **reference** from/to something.
# Unity Basics
- ## General
	- **Unity** is based on a **component** system which means that every **object** in the **scene** has **components** that describe it's behavior
	- **Unity** is both a **2D** and a **3D** engine
	- **Unity** uses **C#** as it's main programming language but is written in **C++**
	- Common misconception is that **Unity** can't have nice visuals and it came from a fact that it's easy to learn and most beginners use it which resulted in a ton of games that don't have decent looking assets
	- Use name
- ## Windows
	- **Scene View** displays all the **objects** currently present in the **scene**
	- **Game View** displays the **current camera** and it's a place in which you'll do all the in-engine playtesting
	- **Hierarchy** is a list of all the **objects** in the **current scene**
	- **Inspector** displays all the **info** and **components** attached to a selected **game object/s**
	- **Project** displays all the **folders** and **files** in your **project**
	- **Console** displays all the **debug** info
	- **Package Manager** is a window in which you'll manage all the **project packages**
- ## Project
	- Make sure that the **Event System** is present in the **scene** to avoid any potential **bugs**
	- Create a **Plane** and scale it to the desired size(use the link feature to scale proportionally)
	- Add a **Capsule**, rename it to **Player** and move it to a desired location
	- Add a **Scripts** folder
	- Create a new **C# Script** and name it **PlayerMovement**
	- 
# Tips
- Keep the **project structure** clean and organized
- Use **namespaces**
- Try to figure out **logical problems** on your own but consult [documentation](https://docs.unity3d.com/ScriptReference/) and experienced people if you are unfamiliar with the concept
- Watch **devlogs** and other game development related content
- Get a firm understanding of **C#**
- Whenever you see something, try thinking of a way you'd implement it in a game
- Don't rely on **GPT** when it comes to writing code but absolutely ask it about the concept or even how your code can be improved
- Follow the **C#** [naming conventions](https://github.com/ktaranov/naming-convention/blob/master/C%23%20Coding%20Standards%20and%20Naming%20Conventions.md)
- Ask people for **feedback** and prompt them with targeted questions