# Version 1.1.11 - Forgot to disable code
- Fixed "This is not a registered game setting" error

# Version 1.1.10 - DAS but I've Never Heard of Her
- Fixed an issue with DAS 5th Edition, where the system disabled the default scrolling behavior on the Client Settings windows. simply Restored the default behavior when using MM+...
> Literally, this patch note is longer then the fix. lol

# Version 1.1.9 - Bugs Where?!?!
- Added the ability to save settings accordion state to remain open on refresh.
- Potentially Fixed changelogs breaking if the module is removed but changelog was tracked.
- Fixed issue with getting system file if it doesn't exist.

# Version 1.1.8 - Just a Little
- Potentially Fixed an issue when a module title is unable to be found
- Updated French Translation

# Version 1.1.7 - A little More Subtle
- Added French Localization (Thanks @Sasmira)
- Added Support for Warhammer Fantasy Roleplay 4th Edition's UI
- Added Option to get Global Conflicts file that is enabled by default. This will prevent MM+ from grabbing globally defined conflicts. Disabling this setting may result in less conflicts notifications.
- Fixed `.settings-list` class in Configure Settings to have a min/max height of 75vh. This should resolve double scrollbars from multiple modules.
- Fixed Socket Settings adding a global `.form-group` to the start of the Module Settings window. This setting will be be styled similar to a module header.
- Fixed Long settings names breaking settings page layout.
- Changed the notify conflicts logic on the Manage Modules button, to only show a conflict number related to active conflicts not all conflicts.

# Version 1.1.6 - Conflicting Module Must be installed
- Fixed an issue that wasn't checking if the conflicting module was installed cause MM+ to register the conflict as a known issue. Now if its a conflict both modules must be installed.

# Version 1.1.5 - Screw Your Emoji
- Added a semxy new settings screen that allows you to filter down to a setting via a search and made it so that settings are grouped into accordion-like elements. This design was HEAVILY influenced by the amazing [TidyUI Game Settings](https://foundryvtt.com/packages/tidy-ui_game-settings) module
- Added Screw Your Emoji which sorts modules and settings
- Added Setting for Full Height Module Management and Configuration Settings
- Added 🧙 Developer Mode Debug Options to make it easier to find issues users are experiencing with not seeing conflicts.
- Fixed an issue where issues were not registering in the tooltips.
- Fixed some UI designs and spacing

> **WARNING** Please be advised that TidyUI and MM+ provide almost the identical functionality. Though MM+ does its best to remain compatible with TidyUI, this is impossible to do so given how we both edit the settings page. MM+ has disabled its settings page in favor of TidyUI. This may not always be the case.

![image](https://user-images.githubusercontent.com/564874/152625472-04f4c4c6-852c-43c5-8b63-3aebfcf34cd7.png)

# Version 1.1.0 - Module Presets
- Added the ability to create, update and delete presets. A preset simply toggles a predefined list of modules as active and disabling all other modules.
- Added the ability to export and import module lists. Exporting will export the `client` and `world` settings for those modules. Importing will allow you to import those settings. Provided support to import `JSON` files created by TidyUI.
> **WARNING** The ability to import settings is considered experimental. Basically I am deleting/removing settings from foundry and replacing them with new ones. In theory this should work just fine, but I can't promise this will work perfectly. Please let me know of any issues you run into.
- Added the ability to toggle all modules (in)active.
- Added URL tag that if a module has the property `url`, clicking this tag will open that URL
- Added Socket tag if module has the property `socket` set to `true`
- Added a Library tag if module has the property `library` set to `true`
- Added `baseUrl` when rendering `README.md` or `CHANGELOG.md` files to better support relative path's for these files. This still requires the module developer to package these images with their module.
- Added the ability to toggle Package Description individually.
- Moved the setting to track Read Changelogs to a client variable so that if you read a changelog in one world, you don't have to re-read it in another world.
- Fixed Conflict(s) UI on manage button to be less invasive and improve compatibility with UI modules
- Fixed Authors property if module developer uses it as a string array instead of an object
- Fixed Internal Debugging methods using 🧙 Developer Mode 
- Removed `github` from issues tag as not everyone uses github/gitlab for issues

# Version 1.0.3 - Little Patches
- Add the ability to show both the 🐛 Bug Reporter tag and a tag linking to bugs url.
- Fixed global conflict url using `http`
- Fixed conflicts with modules not installed registering as a known conflict instead.
- Fixed issue with 🐛 Bug Reporter saying module does not support it.

# Version 1.0.2 - People using author property incorrectly
- Added a fix that will stop the module from crashing if people use the `author` property in an manner I am unware of.
- Added a 🧙 Developer Mode `error` to see the conflicting module.

# Version 1.0.1 - Conflicts with Foundry
## IMPORTANT UPDATE REGARDING PACKAGE MANIFEST+ SUPPORT
[Package Manifest+](https://foundryvtt.wiki/en/development/manifest-plus) is a wondeful set of guidelines that I am attempting to implement support for with this module. However as of January 30th 2022 their guidelines want you to add the properties directly into the root of your `module.json` file. This has been deprecated by foundry in favor of using the `flags` property. MM+ will be going forward assuming you are defining your conflicts and issue inside of the `flags` property. They are defined exactly the same, just within that property. Defining these values outside of the `flags` has been considered **DEPRECATED** by me and may stop working in future versions if MM+.

## Whats Changed/Added?
- Added the ability to list a conflict with foundry
- Added a flag under `"MMP": { "enableFoundryConfirm": true }`, using this flag will present the user with a dialog asking them to confirm enable the module if it conflicts with their version of foundry
- Fixed the tag when there is a conflict with foundry to instead of showing an Explantion Mark and Yellow Tag, it will now show a skull and the tag will be Red

To List a conflict with foundry you must define it under conflicts. Unlike other conflicts, this does not require you to define a name, however it does require that you define they type as foundry.
```json
"flags": {
  "conflicts": [
    {
      "type": "foundry",
      "description": "This module does not support founrdry version 9+. Enabling this module will have issues, due so at your own risk as this version is not supported at this time.",
      "versionMin": "9"
    }
  ]
}
```

# Version 1.0.0 - Module Management+
Module Credits has been rewritten from the ground up with all new features and what I'd like to think as better code and organization. This little project of mine has grown a lot since I started it and foundry even implemented its condensed tags as a core feature. But with its Growth I've decided, I'd just rebrand and release an official version 1 as I am pretty happy with the result. Instead of listing what has changed, I am going to list the all of the features packed into Module Management+
- Condensed the tags on the Module Management window to show just the icon instead of the text. This cleans up the interface and provides more space for longer names. As this is included in Foundry VTT 9.245+ this feature essentially backports it earlier versions of Foundry.
- Added New tags to the packages listed in the Module Management window, these tags are Changelog, Readme, Issues and Authors.
  - Changelog and Readme tags will only show if you are able to access to the `File Browser` permission. However if you have [socketlib](https://foundryvtt.com/packages/socketlib) it will attempt to execute these fuctions as the GM to provide this ability to players who do not have access.
  - The Issues tag provides built in support for 🐛 Bug Reporter, meaning if the module supports but reporter you will be presented with a dialog to file an issue directly in foundry, otherwise it will open a url to the `issues` link the the `module.json` file
  - Authors when clicked will bring up a dialog with a list of all authors in the `module.json` and display links or any information the authors have listed their.
- Cleaned up the interface for the Module Management window, by remove the text that basically said here is where you enable modules, and udpating the css for the filter search/buttons.
- When opening the Module Management window, the filter modules input will automatically be focus to allow you to quickly start typing.
- If a user is unable to manage modules, Ive reworked the interface, to only show active modules and removed the checkbox (which was disabled, but unnessary).
- Added Stripped rows to the packages to make the interface nicer on the eyes and provide seperation of content. Also updated the UI to allow a little more spacing for the same reason
- Added the ability to register and display Conflicts and Known Issues. If a conflict or known issue is defined in a modules `module.json` file or the [global file](https://github.com/mouse0270/module-credits/blob/master/conflicts.json) and the conflict is valid for the versions you have installed, it will be displayed with an ⚠️, hovering over this icon will show a list of all registered conflicts and known issues for that module related the packages installed in your instance of foundry.

# Version 0.0.4.0 - Plus more Options
- Updated to latest version of Foundry.
- Added support for Languages Tag
- Fixed `min-width` for condensed tags for Version and Compatibility Risk 
- Added Popper to allow author tags to support multiple items
- - Author tags will show a list of links or values the author of the module has included
- Fixed compatibility issue DF Chat Enhancements and Module Credits
- Added Option to Condense Author Tags if more then one Author

# Version 0.0.3.2 - Supporting Authors Again
- Fixed behavior when clicking on author. It will now take you the the authors url when clicked.

# Version 0.0.3.1 - Linux Case Sensitive File System
- Fixed an issue with Linux where the file system is case sensitive. Module Credits now uses `FilePicker` to get the correct path. Thank you LorduFreeman for helping me fix this issue

# Version 0.0.3 - All the Customization
Added Option to add font awesome icon to default tags such as Javascript, CSS and Compendium.
Added Option to condense tags. Condensing a tag will remove the text from the tag and only show the icon for that tag.
- Condensing Default Icons requires that you enable the option for default tags to have an icon
- Condensing Module Credits tags will exclude tags that reference outside sources and authors
- Condensing Compatibility Risk tag will add an icon and remove the text `Compatibility Risk` but keep the version text there
- Condensing Version tag will replace the text `Version` with the first character and remove the space between the text and number

Added the ability to load local `readme.md` files within foundry if they are provided
- Please note depending on how the module `readme.me` file references images, they may or may not load.

## Version Tracker
Module Credits will now track version and `changelog.md` files, so if a modules update and they include a `changelog.md` file, module credits will display a list of all updated mods including a `changelog.md` file. Please note that this feature requires module developers to soft opt in by providing a `changelog.md` file with there modules.
- Added Module Changelogs button to **Help and Documentation** section of the side bar, to see all changelogs for all supported modules.

# Version 0.0.2 - MORE TAGS
In this update the module has added the option to add a tag for bugs/issues, wiki/readme and changelog. If the `module.json > [readme, bugs, changelog]` url is setup the module will add colored tags for these options.

This version also include an option to display a local `changelog.md` file within foundry as well. If both `module.json > changelog` and a local `changelog.md` file exists, it will load the local changelog in a window in foundry.

Module Credits now uses [Marked.js](https://github.com/markedjs/marked) and [DOMPurify](https://github.com/cure53/DOMPurify) to allow for local `changelog.md` parsing. This feature is also used to allow users to use markdown and html within their localization for module settings. This feature will most likely be moved into its own library in a future release.

- Added Setting to allow you to show Wiki/Readme tag
- Added Setting to allow you to show Bugs/Issues tag
- Added Setting to allow you to show Changelog tag
- Added Setting to read local `changelog.me` file
- Fixed the border color to `black` to match the default foundry style... Yes I hate it... but I really don't want to change default foundry styles.

# Version 0.0.1 - Initial Release
This module adds a tag to the **Manage Modules** window that list the authors of the module. If the author has a url, it will make the tag a clickable link to that url.

This Module also checks to see if the module has a link listed in the, if it does, it will make the version tag of the module a clickable element as well. Click on this element will open the `module.json > url` property in a new browser tab.
