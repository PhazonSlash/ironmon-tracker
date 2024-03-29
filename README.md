# README #

### IronMON Tracker for Generation 1 and 2 Pokémon games ###

This is a Pokémon stat tracker designed to be used for the [IronMON](https://gist.github.com/valiant-code/adb18d248fa0fae7da6b639e2ee8f9c1) challenge.
The program utilizes a LUA script that runs in the BizHawk emulator in order to extract information from the game's
RAM and displays it in a separate window written in Python.

* The tracker always displays the following information
  * Lead Pokémon Information
    * Pokémon Nickname or Name
    * Type
    * Current Level / Evolves At
    * Current HP / Total HP
    * Number of Moves Learned / Total Moves Learnable
    * Level of Next Learned Move
    * Total Percentage of Heals / Total Number of Healing Items in Bag
    * Current Held Item (Gen 2)
    * Stats and Base Stat Total
  * Lead Pokémon Moves
    * Move Name
    * Type
    * Current PP
    * Power
    * Accuracy


* The tracker conditionally shows the following information
  * Number of attempts at challenge (Enabled in Settings)
  * Three Favorite Pokémon sprites (Enabled in Settings)
  * Enemy Pokémon Information (In Battle)
    * Name
    * Level
    * Base Stat Total
    * Type
  * Wild Pokémon Information (In Battle, including enemy info from above)
    * Number of Moves Learned / Total Moves Learnable
    * Level of Next Learned Move
    * Evolves At


### Setup ###

* Download the latest release of this tracker and extract all files to a folder
* Download [BizHawk](https://tasvideos.org/Bizhawk) emulator
* Install [Python](https://www.python.org/downloads/) version 3.8 or later
* Install Python Dependencies
  * For Windows users, run the Setup_Windows.bat file
  * For other platforms, run the following terminal commands from the tracker's root directory
    * >pip install pygame
    * >pip install numpy
      
### Running the Tracker ###

* Open the Tracker Program
  * For Windows users, run the Start_Tracker_Windows.bat file
  * For other platforms, run the following terminal command from the tracker's root directory
  * >python tracker.py
* If successful, you should see the tracker with no data filled out

### Using the Tracker with Your Game ###

* Open BizHawk and load your game ROM file
  * Tracker supports the following games, only English ROMs have been tested
    * Pokémon Red Version
    * Pokémon Blue Version
    * Pokémon Yellow Version
    * Pokémon Gold Version
    * Pokémon Silver Version
    * Pokémon Crystal Version
* In BizHawk, select Tools from menu bar and then select Lua Console
  * In the Lua console, select Script from menu bar then select Open Script
    * Navigate to the folder containing the tracker files and open tracker.lua
  * Upon loading, there should be a message in the Lua console with your game version

### Configuring the Tracker ###

* Keybinds

Key Combination | Action
------------- | -------------
Ctrl+Q  | Close Tracker Program
Equals OR NumPad-Plus  | Increment Attempts
Minus OR NumPad-Minus  | Decrement Attempts
Ctrl+R OR Ctrl+NumPad-0 | Reset and Increment Attempts
Ctrl+M  | Load random mail message
Ctrl+S  | Save current mail message to file
Backspace  | Open/Close(and save) Settings Menu
Up/Down Arrow  | Navigate Settings Menu
Left/Right Arrow Key or Click OR Scroll Wheel on Mouse Over  | Change Settings in Menu

* Settings
  * You can edit most of these in the tracker by pressing the Backspace key or clicking the little Pokéball on the top right. You can use a mouse or arrow keys to select/change settings. Press Backspace or click outside the menu to close and save.
  * Some settings can only be changed by opening settings.json in a text editor and manually changing the values. Remember to save and restart the tracker.

Setting | Description | Values
------------- | ------------- | ------------
showFavorites  | Displays sprites of favorite Pokémon | true or false
favorites  | Define what favorite Pokémon to show | enter 3 different national dex numbers as strings (in double quotes) separed by commas
showAttempts  | Show number of attempts at challenge | true or false
attempts  | Current number of attempts | a positive whole number representing number of attempts
rbColor  | Enable to show Pokémon Red/Blue sprites in Super Game Boy color pallet | true or false
randomMail  | See Mail Randomizer section below  | true or false
borderType  | The type of frame used to border the moves | a whole number representing the frame type. If -1, then it will load frame from game. Frame 0 is the Gen 1 frame. Frames 1 through 8 are the Gen 2 borders.

### Mail Randomizer ###

This is an optional feature exclusive to the generation 2 games and requires changing a setting in the randomizer.
If enabled and your starter Pokémon comes with a held mail item, you can load a random message into the mail item.

Disclaimer:
This is purely for fun and serves no benefit to the player.
In a way, it may make the game a bit harder because you will lower your chances of starting with a good item.
This will directly modify in-game RAM values, specifically the data stored in addresses related to mail items.
This is the only feature of the tracker that can write data to the game's memory.
While this offers no benefit to the player, some may take issue with an outside program manipulating the game's memory.
This also technically changes the official IronMON randomizer settings in a minor, but still game changing way, so some may view this violating the rules of the challenge.
Use at your own discretion.

To use the mail randomizer:

* Open the settings.json file into a text editor, set randomMail to true, and save.
  * > "randomMail": true
* In the randomizer settings, you must disable Ban Bad Items for your starter Pokémon. This will give your Pokémon a chance to start with a mail item. This also means that you will have a lower chance of starting with a good item.
* As soon as you get your starter Pokémon, the message of their mail item will be overwritten with a random message.
* The messages are selected from the file '/json/mail.json'. You can edit this file directly to remove messages. Adding new messages directly to this file is not recommended.
* You can add new messages to the pool of random messages in game. To do this, follow these steps:
  * Give a mail item to the Pokémon in your first party slot.
  * Write whatever message you want to save into the mail item using the in-game mail editor.
  * Click on the tracker and press the 'Ctrl' and 'S' keys at the same time to write to the file.
  * You can test loading random messages into the slot 1 Pokémon's held mail by pressing 'Ctrl' and 'M' keys at the same time in the tracker. If you are still reading the old mail in-game, you must back out and select Read on the held mail again.