# Dialog Selector

The Dialog Selector plugin allows you to create a rudimentary branching dialog system using a plugin setting for configuration of npc dialog per map.  Dialog can also be set up to requiire certain swtiches to be active in order for that dialog to be shown.  When used in combination with some eventing, you can create a basic dialog system.


Plugin Version: 0.5

[Plugin Demo](http://www.lmpgames.com/RMMV/Plugins/Demos/LMPGames_DialogSelector_Demo_V0.5.1.zip)

[Plugin Project](http://www.lmpgames.com/RMMV/Plugins/Projects/LMPGames_DialogSelector_Project_V0.5.1.zip)


## Installing the plugin
Download the plugin file either using the Demo or Project links above or from the repository.  Please the .js file into your js/Plugins folder and then add the plugin into your project in the Plugin Manager screen.

Note, YanFly_MessageCore is highly recommended but optional.


## Plugin Information
This section contains information relating to plugin settings and commands used with plugin.  To learn how to use and what certain commands or settings do, continue reading.  If you are looking for configuraiton information, see the Configation Settings section below.


### Plugin Settings

#### Enable Dialog System
This setting controls whether or not the dialog system is enabled when the game starts.  Set this to true to enable the system at the start of the game.<br>
Boolean<br>
true<br>


#### Text Game Variable
This setting sets the game variable that will be used to store the current npc dialog to display.<br>
**Required**<br>
Game Variable<br>
001


#### Map Data
This setting contains the configuration for each map and each npc on those maps that the Dialog System should apply to.  For more information on how to configure this setting, see the Configuration Settings section below.<br>
**Required**<br>
Object


#### Default Dialog
This setting sets the dialog shown by an NPC when there is no valid dialog available to be shown.  This only applies to configured NPCs.  Please note that the ESC character is used; do not change this.<br>
Text<br>
Hello, \P[1]


#### Unconfigured NPC Dialog
This setting sets the dialog to be displayed when calling the plugin command from an NPC that either has not figured for the current map or whose map is not configured in the Map Data plugin setting.  This is meant to be used as a development debugging tool, an option to turn this output off or on will be added in a future version.<br>
Text<br>
This map or npc has not been configured in the Dialog Selector plugin configuration data.



### Plugin Commands
#### Tutorial.DialogSelector GetDialog <MapId> <NpcId>
This plugin command allows you to call the GetDialog function to get the current valid dialog for an NPC on a specific map.  Note that Map Id must be the id of the current map the NPC event is currently on or the system will show the text set in the Unconfigured NPC Dialog setting.

**Parameters**
- MapId
  - Sets the ID for the map that the current NPC is on.  Must match the ID for the currently map.
- NpcId
  - Sets the NPC ID that plugin should look for to find the proper dialog configuration for.

**Example**
```
LMPGames.DialogSelector GetDialog 1 2
```


#### LMPGames.DialogSelector EnableDialogSystem <0/1>
This plugin command allows you to enable or disable the dialog system from an NPC within the game.  0 means that the system is disabled, while 1 means that the system is enabled.

**Parameters**
- <0/1>
  - 0 = Disabled / 1 = Enabled

**Example**
```
LMPGames.DialogSelector EnableDialogSystem 0
```



### Configuration Settings
This section will detail how to configure the Map Data plugin setting for use with the plugin.

#### Map Configuration
The first level of configuiration is to set up the configuration records for each map that will contain NPCs that are a part of the dialog system.  If an NPC does not use the GetDialog plugin command, it does not need to be configured here and if no NPCs on a map use it either then the map doesn't need to be configured here either.

The first step is to identify the Map ID for the map you're configuring.  You can find this, easily, by looking at the bottom of the editor window.  In the footer bar on the right side you should see some values, of which the left most one is your map id and name.  Use this map id for the Map Id setting.

Next you'll need to set up the NPC configration settings for each NPC on the map that will use the system.  Double click on the Npc List setting.


#### NPC Configuration
This is the second level of configuration for the plugin.  Here you will, like you did with the Map Configuration, locate the NPC Id for the NPC you are going to enter dialog configuraiton for and place that ID into the Npc Id setting.  This can be found in the NPC event window in the editor in the top left corner of the event window.

Once you have this, you'll need to configure the dialog settings for this specific npc.  Double click on the Dialog List setting.


#### Dialog Configuration
This is the final level of configuration for the plugin.  To configure dialog for use by the NPC create new rows by double clicking in an empty space in the list.  You should then see a window with the Conditions and Dialog settings.

Dialog is the text that the NPC should use when the conditions are met.

Conditions is the list of switches that should be turned on in order to the NPC to use this specific dialog.  If there should be no conditions, such as for setting up default text, then leave the Conditions setting set to the default value.  Please be aware that conditions in the Conditions setting are checked in reverse, just like event pages.  If you place an dialog setting with no conditions at the bottom of the conditions list, that is the only dialog that will be displayed by the NPC.

When adding Conditions, you will be asked to select the Switch from a drop down.  It is advisable to separate your dialog switches from your other switches and to name them at this point so that they can easily be found and understood later when setting up any additional event configuration that you may require.

##### Text Codes
Text codes are supported in dialog text configured within the plugin.


**For more specifics on how this data can be configured, see the plugin project for examples**



## Planned Future Enhancements
- Ability to turn on or off YanFly_MessageCore support
- Ability to turn on or off Unconfigured NPC Dialog setting
- Effeciency enhancement to load only the data from the map you are currently on
- New Setting<br>
  - Data Load Mode<
    - First mode will load the data from the Map Data plugin setting
    - Second mode will allow you to load data from a file
      - Details on file structure and how these files line up with map/npc ids tbd but the goal is to reduce the complexity to use the plugin down to nearly 0.


## Possible Enhancements
None at this time


## Conflicts
Any plugin that overrides or aliases Window_Base.convertEscapeCharacters may conflict with this plugin without integration/a patch.


## Change Log
- Version 0.5.1
  - Fixes
    - Fixed an issue where NPC Ids over 1 digit were being cut off by the plugin command

- Version 0.5
  - New Features
    - Support for text codes within the dialog configuration.
	- Confirmed that MessageCore functionality works from dialog configuration.

- Version 0.1
  - Initial version of plugin


