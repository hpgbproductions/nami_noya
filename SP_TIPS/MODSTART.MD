### Mod Start Checklist

- Setup
  - Check scripting backend is Mono and .NET API compatibility level is 4.x.
  - Import mod tools (drag Unity package from SP folder or Jundroo folder from a recent mod).
  - Import SP assets pack if desired.

- For mods with scripts
  - Add Service Provider using SimplePlanes tab on top menu.

- For mods with visible objects
  - Enable fog in top bar > Rendering > Lighting window
  - In Preferences, enable OpenXR and set strip shaders to none (guide for this is missing on SP forums?)

### Troubleshooting

- **Prefab does not exist when saving GameObject**
  - Check for missing scripts or assets in the GameObjects. They may have been deleted accidentally.
- **OpenXR validation issues when attempting to build mod**
  - Go to the log and find the message that allows you to double-click it to fix the issues. Click on the "Fix" button to fix the error. While this changes the target platform from "PC, Mac and Linux" to only "PC", there have not been any negative effects reported by Mac users.
- **Failed to load a mod, with red wall of text**
  - Check scripting backend is Mono and .NET API compatibility level is 4.x.
- **Stuck on loading screen**
  - Check log for SerializationException. This type of exception can happen when the list of public or serialized private fields and properties is changed without saving the GameObjects.
- **EasyRoads3D roads don't appear**
  - Ensure road assets are stored in the project folder after entering Build Mode. (Road Network component > Update Terrain (horizontal bar menu) > Store Mesh Assets)
- **EasyRoads3D roads cause cars to get stuck**
  - Do not assign a Physic Material to the roads.
