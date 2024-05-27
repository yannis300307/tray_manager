# What is tray_manager ?
TrayManager is a package for adding a system tray icon, based on pystray (https://github.com/moses-palmer/pystray by Moses Palmér), this package is an "easier" version of pystray to manipulate based on the use of object (Object Oriented Programming).

# Usage
1. [Create a TrayManager object]("https://github.com/Adastram1/tray_manager/blob/main/README.md#create-a-traymanager-object")
2. [Create and interact with Items]("https://github.com/Adastram1/tray_manager/blob/main/README.md#create-and-interact-with-items")
3. [Add items to the Menu]("https://github.com/Adastram1/tray_manager/blob/main/README.md#add-the-items-to-the-menu")
4. [Customize the TrayManager object]("https://github.com/Adastram1/tray_manager/blob/main/README.md#customize-the-traymanager-object")
5. [Customize and edit the items]("https://github.com/Adastram1/tray_manager/blob/main/README.md#customize-and-edit-the-items")
6. [Check for OS supported features]("https://github.com/Adastram1/tray_manager/blob/main/README.md#check-for-os-supported-features")
7. [Notifications]("https://github.com/Adastram1/tray_manager/blob/main/README.md#notifications-currently-unavaible") [CURRENTLY UNAVAIBLE]
8. [Advanced settings]("https://github.com/Adastram1/tray_manager/blob/main/README.md#advanced-settings")
9. [Examples]("https://github.com/Adastram1/tray_manager/blob/main/README.md#examples")

## Create a TrayManager Object
The main object of the librairie is the TrayManager object, it is the central element and can be considered as the icon in the system tray itself, it contains all the elements of our app.

To create one, you need to import the tray_manager.TrayManager class and create a tray object as followed :
```python
from tray_manager import TrayManager
tray = TrayManager(app_name="My App")
```

## Create and interact with Items
The items are the elements of your app, they will be displayed in the menu they're added to. Their is different kinds of items that all works in a similar way but each have some specificities. 

Here is the list of all the items :
1. [Label]("https://github.com/Adastram1/tray_manager/blob/main/README.md#label")
2. [Button]("https://github.com/Adastram1/tray_manager/blob/main/README.md#button")
3. [CheckBox]("https://github.com/Adastram1/tray_manager/blob/main/README.md#checkbox")
4. [Separator]("https://github.com/Adastram1/tray_manager/blob/main/README.md#separator")
5. [Submenu]("https://github.com/Adastram1/tray_manager/blob/main/README.md#submenu")

### Label
The label is the most basic item, it is only constituated of a text.

To create one, you need to use the tray_manager.Label class as followed :

```python
from tray_manager import Label
my_label = Label("My Label")
```



### Button
The button is like the label item but you can add a callback argument (FunctionType) that will be called when the user clicks on the button. You can also specify some arguments as a tuple that will be passed too your function when the callback runs.

To create one, you need to use the tray_manager.Button class as followed : 

```python
from tray_manager import Button
def my_callback(text: str) -> None:
  print(text)

my_button = Button("My Button", my_callback, args=("Hello",))
```



### CheckBox
The CheckBox item is a bit more complex than a regular button, it has 2 differents callbacks instead of 1 and different arguments for each, one for when the checkbox switch from the 'Disabled' to 'Enabled' state (Not checked to checked), and one for when it switch from the 'Enabled' to 'Disabled' state (Checked to not checked).

You can 'Disable' the interactions with your checkbox by setting the value of check_default to None (Note : The callback won't be called if the user clicks on the checkbox when it is disabled).

To create one, you need to use the tray_manager.CheckBox class as followed :

```python
from tray_manager import CheckBox

def checked(text: str) -> None:
  print(f"In procedure 'checked' : {text}")

def unchecked(text: str) -> None:
  print(f"In procedure 'unchecked' : {text}")

my_checkbox = CheckBox("My CheckBox", check_default=False, checked_callback=checked, checked_callback_args=("I'm now checked",),
                        unchecked_callback=unchecked, unchecked_callback_args=("I'm now unchecked",))
```

To get the current state of the checkbox (checked : True | unchecked : False | disabled : None), you can use the .get_status() function as followed :

```python
from tray_manager import CheckBox

my_checkbox = CheckBox("My CheckBox")

my_checkbox.get_status()
-> bool | None
```

You can also set the state of the checkbox by using the .set_status() function as followed : 

```python
from tray_manager import CheckBox

my_checkbox = CheckBox("My CheckBox")

my_checkbox.set_status(True)
-> Checked
my_checkbox.set_status(False)
-> Unchecked
my_checkbox.set_status(None)
-> Disabled
```



### Separator
The separator is a built-in object of Pystray, it doesn't require any parameters.

To create one, you need to use the tray_manager.Separator class as followed : 

```python
from tray_manager import Separator
my_separator = Separator()
```



### Submenu
The submenu is like a Menu() object and can contains other items including other submenu. Be carreful when adding submenu into each others as adding a submenu to itself will generate an tray_manager.CircularAddException error.

To create one, you need to use the tray_manager.Submenu as followed : 

```python
from tray_manager import Submenu
my_submenu = Submenu("My Submenu")
```

To add an item to the submenu, you can use the .add() function as followed : 

```python
from tray_manager import Submenu, Label
my_submenu = Submenu("My Submenu")
my_label = Label("My Label")

my_submenu.add(my_label)
```
To remove an item to the submenu, you can use the .remove() function as followed : (Note : The .remove() function returns the item that was removed) 

```python
from tray_manager import Submenu, Label
my_submenu = Submenu("My Submenu")
my_label = Label("My Label")

my_submenu.add(my_label)

my_submenu.remove(my_label)
-> my_label
```


To get the items contained in a submenu, you can use the .get_items() function as followed:

```python
from tray_manager import Submenu, Label, Button

def my_callback()
  print("Hello")

my_submenu = Submenu("My Submenu")
my_label = Label("My Label")
my_button = Button("My Button", my_callback)

my_submenu.add(my_label)
my_submenu.add(my_button)

my_submenu.get_items()
-> [my_label, my_button]
```

## Add the items to the Menu

## Customize the TrayManager object

## Customize and edit the items

## Check for OS supported features

## Notifications [CURRENTLY UNAVAIBLE]

## Advanced settings

## Examples
