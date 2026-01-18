## Important rules
Never manually position a camera that is driven by a distance variable.

## Unity Things to Remember
Basic Variable syntax for unity
* `[access] [type] [name] = [value];`
Example
* `private float speed = 5; // Floats MUST end with an f if the float has a decimal value such as 5.1`

For basic C# knowledge, statements, field declarations/definitions, and method declarations need semicolons at the end of each line, but a few other things
properties, method definitions, type definitions, for example, don't.

Variables for the inspector should have a [SerializeField] before the [access]. This is the correct way to make variables that are editable in the inspector. Recommended to keep private unless I actually want the variable to be accessible by other scripts.
Example:
* `[SerializeField] private string Something = "Hello World";`

At the top of the class, if I want to force the object to require a specific component, such as Rigidbody, add `[RequireComponent(typeof(COMPONENT_TYPE)]`which forces the object to use that component

To lock the mouse to the game, inside of Start() add:
* Cursor.lockState = CursorLockMode.Locked; 
* Cursor.visible = false;


## Functions to get the script started.

Runs first (initial setup)
* void Awake()

Runs once before first frame
* void Start()

Runs every frame (input)
* void Update()

Runs on physics tick
* void FixedUpdate()

OnEnable()
* lifecycle method that runs when the GameObject becomes active(just before it starts running each frame)

OnDisable()
* Runs when the GameObject or component is disabled or destroyed.

InputActionsAsset
* Contains Action Maps(groups of related actions such as Movement), Actions(individual controls like Move and jump), Bindings(Keys/buttons that trigger an action)

Quick Mental Model (Keep This)
* Variables = state
* Inspector = tuning
* Scripts = behavior
* GameObjects = containers

Print in Unity is `Debug.Log()`. Debug is Unity-specific API.
Inside `Debug.Log()`, use a `$` before the quotes and add curly braces inside the quotes to print strings with variables.
example: `Debug.Log($"Godmode is currently {godMode}");`

Temporary variables are simply made via `[type] [name] = [value];` They don't use `[access]` or the `[SerializeField]` prefixes.

Example: `int number = 0;`

## Input Related

`InputActionAsset`
* A serialized asset that defines the ACtions Maps, Actions, and bindings.
* Used to centralize input configuration (keyboard, gamepad, etc.)

`FindActionMap()`
* An InputActionAsset can contain several action maps.
* `FindActionMap("Name", true)` lookup an action map by name and returns it.

`FindAction()`
* returns the InputAction based on the name. 
* If the name is invalid the true flag throws an error.

`Enable()`
* InputSystem property that starts listening for input events on all actions in the specific map
* Without calling Enable(), none of the actions will produce values.
* Enabling the map activates all its actions.

`InputAction.ReadValue<T>()`
* If an action has multiple bindings (e.g., WASD + gamepad stick), ReadValue() returns the combined value from all relevant devices.


## Common Functionalities

`GetComponent<T>()`
* A method that retrieves another component attached to the same GameObject.
* T is the component type like RigidBody and such.
* Used in the Awake()

`Normalize() / .normalized`
* Converts a vector to length 1, preserving direction.
Example:
* `(1, 0, 1) → magnitude ≈ 1.414`
After normalization:
* `(0.707, 0, 0.707) → magnitude = 1`

`transform.forward`
* A direction vector representing where an object is facing.
* Updates automatically when rotating.

`Mouse.current.delta.ReadValue()`
* Reads the mouse movement since the last frame.
* Return X and Y values for horizontal and vertical mouse movement respectively.

`Mathf.Clamp()`
* Limits a value between a minimum and maximum
* Used for pitch (example)

`Quaternion.Euler()`
* Creates a rotation from Euler angles(Degrees)
**Important clarification**
* You are not rotating with Euler angles.
* You are creating a quaternion from Euler angles.

`transform.eulerAngles`
* A human readable representation of rotation in degrees
