
# How to Install Minecraft Bedrock Addons on a BAO Server

This guide explains how to install Minecraft Bedrock addons manually using the BAO server file manager.

It is written for beginners. Follow the steps in order, and do not skip a step if you are installing addons for the first time.

## Before You Start

Make sure you have:

- Access to your BAO server panel and file manager.
- The addon you want to install (`.mcaddon`, `.mcpack`, or `.zip`).
- A way to extract or unarchive files.
- A backup of your world and the existing pack registration files.

> **IMPORTANT:** Stop your server before editing its files. Back up your files first so you can restore them if something goes wrong.

## Understanding the Important Files

Before installing anything, understand these three things:

| File or Folder | Purpose |
|---|---|
| `behavior_packs` | Stores Behavior Packs that control gameplay, entities, items, recipes, and other behavior. |
| `resource_packs` | Stores Resource Packs that contain textures, models, sounds, and other visual or audio assets. |
| `manifest.json` | Contains information about a pack, including its UUID and version. |
| `world_behavior_packs.json` | Tells the world which Behavior Packs to load. |
| `world_resource_packs.json` | Tells the world which Resource Packs to load. |

**Remember:** Behavior Packs and Resource Packs are different. They must be placed in the correct folders and registered separately.

Some addons require only one pack. Others require both a Behavior Pack and a Resource Pack.

---

# PART 1: Install Your First Addon

## Step 1: Stop Your Server

1. Open your BAO server panel.
2. Stop the Minecraft server.
3. Wait until the panel shows that the server has stopped.
4. Open the file manager.

Do not edit the files while the server is running.

## Step 2: Find Your Active World Folder

Navigate to your active world folder in the BAO file manager.

In your setup, the path may be displayed as:

```text
world → bedrock level
```

Use the active world's folder, not a different world or an unrelated directory.

The examples in this guide assume that `behavior_packs`, `resource_packs`, and the two `world_..._packs.json` files belong inside this active world folder.

Your folder should eventually look similar to this:

```text
bedrock level/
├── behavior_packs/
├── resource_packs/
├── world_behavior_packs.json
└── world_resource_packs.json
```

If the two pack folders do not exist, create them.

**Important:** Some Bedrock server setups also have `behavior_packs` and `resource_packs` folders at the server's main directory. Those folders are for server-wide packs. This guide uses the world-specific folders so that the addon is associated with the selected world.

## Step 3: Upload Your Addon

Upload your addon file to the file manager.

Common file types include:

- `.mcaddon`
- `.mcpack`
- `.zip`

For example:

```text
MyAddon.mcaddon
```

You can upload the file to a temporary folder first, so you can extract its contents without mixing them with your installed packs.

**Do not install the archive itself as though it were an actual pack folder.** You need to extract the files and locate the pack's `manifest.json`.

## Step 4: Extract the Addon Completely

This is one of the most important steps.

A `.mcaddon` file can contain one or more `.mcpack` files. A `.mcpack` file can contain the actual files for a Behavior Pack or Resource Pack.

Sometimes, extracting a file reveals another archive instead of the actual pack folder.

### Example A: You Extract a `.mcaddon`

Suppose you begin with:

```text
MyAddon.mcaddon
```

After extracting it, you might get:

```text
MyAddon/
├── MyAddon_BP.mcpack
└── MyAddon_RP.mcpack
```

You are **not finished yet**.

Extract `MyAddon_BP.mcpack` and `MyAddon_RP.mcpack` separately.

You might then get:

```text
MyAddon_BP/
├── manifest.json
├── entities/
├── items/
└── ...
```

And:

```text
MyAddon_RP/
├── manifest.json
├── textures/
├── models/
└── ...
```

The exact contents will differ between addons.

### Example B: You Extract a `.mcpack`

Suppose you already have:

```text
MyAddon_BP.mcpack
```

Extract that file until you can access the actual Behavior Pack folder containing `manifest.json`.

Do the same for a Resource Pack if needed.

### The Rule to Remember

**Keep extracting until you reach the actual pack folder containing `manifest.json`.**

If you still see a `.mcaddon`, `.mcpack`, `.zip`, or another archive instead of the pack's files, extract it again.

Do not keep extracting ordinary folders once you have reached the actual pack folder.

## Step 5: Identify Which Pack Is Which

You must determine whether each extracted folder is a Behavior Pack or Resource Pack.

### Behavior Pack

A Behavior Pack commonly contains files related to:

- Entities and mobs.
- Items and recipes.
- Loot tables.
- Functions.
- Gameplay mechanics.
- Scripts.

Place the actual Behavior Pack folder here:

```text
bedrock level/behavior_packs/
```

Example:

```text
behavior_packs/
└── MyAddon_BP/
    ├── manifest.json
    ├── entities/
    └── ...
```

### Resource Pack

A Resource Pack commonly contains files related to:

- Textures.
- Models.
- Sounds.
- Animations.
- Text and language files.

Place the actual Resource Pack folder here:

```text
bedrock level/resource_packs/
```

Example:

```text
resource_packs/
└── MyAddon_RP/
    ├── manifest.json
    ├── textures/
    └── ...
```

### If Your Addon Contains Both

Install both packs in their correct folders.

Do not delete the Resource Pack just because you have already installed the Behavior Pack. The addon may need both to work correctly.

If the addon includes only one pack, install only that pack.

## Step 6: Put the Actual Pack Folder in the Correct Location

Let's say you extracted this folder:

```text
MyAddon_BP/
├── manifest.json
└── ...
```

Upload or move the entire `MyAddon_BP` folder into:

```text
bedrock level/behavior_packs/
```

The correct result is:

```text
behavior_packs/
└── MyAddon_BP/
    ├── manifest.json
    └── ...
```

**Do not put the `.mcpack` file inside `behavior_packs` without extracting it first.**

Also, do not accidentally add an unnecessary extra folder.

Incorrect:

```text
behavior_packs/
└── MyAddon/
    └── MyAddon_BP/
        ├── manifest.json
        └── ...
```

Correct:

```text
behavior_packs/
└── MyAddon_BP/
    ├── manifest.json
    └── ...
```

The same rule applies to Resource Packs.

The folder that directly contains `manifest.json` should be inside the corresponding pack directory.

## Step 7: Open the Behavior Pack's `manifest.json`

Open the Behavior Pack's folder and find:

```text
manifest.json
```

For example:

```text
bedrock level/behavior_packs/MyAddon_BP/manifest.json
```

Open the file and look for the `header` section.

Example:

```json
{
  "format_version": 2,
  "header": {
    "name": "My Addon",
    "description": "Example addon",
    "uuid": "11111111-2222-4333-8444-555555555555",
    "version": [1, 0, 0]
  }
}
```

You need two values:

- `uuid`
- `version`

In this example:

```text
UUID: 11111111-2222-4333-8444-555555555555
Version: [1, 0, 0]
```

**Important:** Copy the UUID and version from the `header` section, not from the `modules` section.

Your actual addon will have different values. Use the ones in your own file.

Most packs use a version array such as `[1, 0, 0]`. Copy the actual header version exactly. If your pack uses a different version format, do not guess or convert it; check that the pack and server versions are compatible.

## Step 8: Create or Edit `world_behavior_packs.json`

Go back to your active world folder.

Find this file:

```text
world_behavior_packs.json
```

If it does not exist, create it with that exact filename.

Open it and add the Behavior Pack's UUID and version.

Example:

```json
[
  {
    "pack_id": "11111111-2222-4333-8444-555555555555",
    "version": [1, 0, 0]
  }
]
```

Replace the example UUID and version with the actual values from your Behavior Pack's `manifest.json`.

Save the file.

**Do not put `world_behavior_packs.json` inside the `behavior_packs` folder.** It belongs in the active world folder.

Also, do not copy the example values as your real addon values.

## Step 9: Register the Resource Pack, If Required

If your addon includes a Resource Pack, open its own `manifest.json`.

For example:

```text
bedrock level/resource_packs/MyAddon_RP/manifest.json
```

Find the Resource Pack's own `header.uuid` and `header.version`.

Do not reuse the Behavior Pack's values unless the actual manifest specifically gives the same pack identity.

Now return to the active world folder and find:

```text
world_resource_packs.json
```

Create the file if it does not exist.

Add an entry using the Resource Pack's own values:

```json
[
  {
    "pack_id": "AAAAAAAA-BBBB-4CCC-8DDD-EEEEEEEEEEEE",
    "version": [1, 0, 0]
  }
]
```

Replace both example values with the actual Resource Pack UUID and version from its `manifest.json`.

Save the file.

**Remember:**

- Behavior Pack goes in `behavior_packs`.
- Resource Pack goes in `resource_packs`.
- Behavior Pack registration goes in `world_behavior_packs.json`.
- Resource Pack registration goes in `world_resource_packs.json`.

## Step 10: Check Everything Before Starting the Server

Your files should now look similar to this:

```text
bedrock level/
├── behavior_packs/
│   └── MyAddon_BP/
│       ├── manifest.json
│       └── ...
│
├── resource_packs/
│   └── MyAddon_RP/
│       ├── manifest.json
│       └── ...
│
├── world_behavior_packs.json
└── world_resource_packs.json
```

Check the following:

- [ ] You extracted the `.mcaddon` or `.mcpack` files completely.
- [ ] Every installed pack has its own folder.
- [ ] Every pack folder contains `manifest.json`.
- [ ] Behavior Packs and Resource Packs are in the correct folders.
- [ ] The UUID and version are copied from each pack's `header`.
- [ ] Both JSON registration files are in the active world folder.
- [ ] The JSON files contain valid JSON syntax.
- [ ] You did not delete entries for existing addons.

## Step 11: Start and Test the Server

1. Save every file.
2. Start your BAO server.
3. Wait for the server to finish starting.
4. Join your Minecraft server.
5. Test the addon to see whether it works.

If the addon requires both packs, check that both are registered.

Some addons also need experimental features, Script API support, dependencies, or specific Minecraft versions. Installing the files alone will not guarantee compatibility.

---

# PART 2: How to Install Multiple Addons

You do not need to create a separate `world_behavior_packs.json` or `world_resource_packs.json` for every addon.

**Use one registration file for all Behavior Packs and another registration file for all Resource Packs in the same world.**

Each installed pack gets its own folder and its own entry in the appropriate JSON file.

## Step 1: Install the First Addon

Follow Part 1 to install and register your first addon.

For this example, let's say you installed:

```text
MyAddon_BP
MyAddon_RP
```

Your folders will look like this:

```text
behavior_packs/
└── MyAddon_BP/

resource_packs/
└── MyAddon_RP/
```

The exact pack names can be different.

## Step 2: Extract the Second Addon

Upload your second addon, for example:

```text
AnotherAddon.mcaddon
```

Extract it completely.

If it produces `.mcpack` files, extract those too until you reach the actual pack folders.

Suppose the second addon contains:

```text
AnotherAddon_BP/
AnotherAddon_RP/
```

Place them separately.

Behavior Pack:

```text
behavior_packs/
├── MyAddon_BP/
└── AnotherAddon_BP/
```

Resource Pack:

```text
resource_packs/
├── MyAddon_RP/
└── AnotherAddon_RP/
```

**Do not combine the files from different addons into one folder.** Keep each actual pack in its own folder.

## Step 3: Get the UUID and Version of the Second Addon

Open:

```text
AnotherAddon_BP/manifest.json
```

Copy its `header.uuid` and `header.version`.

Then open:

```text
AnotherAddon_RP/manifest.json
```

Copy that pack's `header.uuid` and `header.version` too, if a Resource Pack is included.

Every pack must be registered using its own correct values.

Do not assume two packs use the same UUID or version.

## Step 4: Add the Second Behavior Pack to the Existing JSON File

Open your existing:

```text
world_behavior_packs.json
```

Do not delete your first addon's entry.

Instead, add a second entry after the first one.

Example:

```json
[
  {
    "pack_id": "UUID-FOR-FIRST-BEHAVIOR-PACK",
    "version": [1, 0, 0]
  },
  {
    "pack_id": "UUID-FOR-SECOND-BEHAVIOR-PACK",
    "version": [1, 0, 0]
  }
]
```

Replace the placeholder UUIDs and version numbers with the real values from each pack's `manifest.json`.

The versions above are only examples. Use the actual versions.

Notice the comma between the two entries. Without that comma, the JSON file will be invalid.

## Step 5: Add the Second Resource Pack to the Existing JSON File

If the second addon also includes a Resource Pack, open your existing:

```text
world_resource_packs.json
```

Keep the first entry and add the second entry.

Example:

```json
[
  {
    "pack_id": "UUID-FOR-FIRST-RESOURCE-PACK",
    "version": [1, 0, 0]
  },
  {
    "pack_id": "UUID-FOR-SECOND-RESOURCE-PACK",
    "version": [1, 0, 0]
  }
]
```

Replace every placeholder with the actual Resource Pack values.

Save the file.

If the second addon does not contain a Resource Pack, do not create a fake Resource Pack entry.

## Step 6: Repeat for Every Additional Addon

Repeat the same process for the third, fourth, fifth, and any other addons you want to install.

For every new addon:

1. Upload the addon.
2. Extract the `.mcaddon` or `.zip` file.
3. Extract any `.mcpack` files produced by the first extraction.
4. Find the actual pack folders containing `manifest.json`.
5. Place each pack in the correct folder.
6. Copy the UUID and version from each pack's `header`.
7. Add each pack to the existing JSON file for its pack type.
8. Save your changes.

You should end up with one entry per installed pack, not one entry per `.mcaddon` archive.

For example, if three addons each include a Behavior Pack and a Resource Pack, you could have:

```text
behavior_packs/
├── Addon1_BP/
├── Addon2_BP/
└── Addon3_BP/

resource_packs/
├── Addon1_RP/
├── Addon2_RP/
└── Addon3_RP/
```

And your registration files would contain three entries each:

```text
world_behavior_packs.json
└── Entry for Addon 1 BP
└── Entry for Addon 2 BP
└── Entry for Addon 3 BP
```

```text
world_resource_packs.json
└── Entry for Addon 1 RP
└── Entry for Addon 2 RP
└── Entry for Addon 3 RP
```

The labels above describe the entries; they are not literal JSON syntax.

## Step 7: Make Sure Your JSON Files Are Correct

A common mistake is forgetting a comma or deleting an existing entry.

For example, this is incorrect:

```json
[
  {
    "pack_id": "UUID-ONE",
    "version": [1, 0, 0]
  }
  {
    "pack_id": "UUID-TWO",
    "version": [1, 0, 0]
  }
]
```

There is no comma between the two entries.

This is the correct structure:

```json
[
  {
    "pack_id": "UUID-ONE",
    "version": [1, 0, 0]
  },
  {
    "pack_id": "UUID-TWO",
    "version": [1, 0, 0]
  }
]
```

The placeholder values must still be replaced with the actual UUIDs and versions before the configuration can work.

**JSON reminders:**

- Put a comma between entries.
- Do not add a comma after the final entry.
- Keep the opening `[` and closing `]`.
- Use double quotation marks around text.
- Do not add comments inside the JSON file.
- Do not paste the entire JSON example below the existing JSON. Edit the existing array instead.

## Step 8: Start the Server and Test the Addons

When you have finished registering all your packs:

1. Save both JSON files.
2. Check the folders and filenames again.
3. Start the BAO server.
4. Wait for startup to finish.
5. Join the server.
6. Test each addon.

When installing many addons, it is safer to install and test them one at a time. If you install ten addons at once and something breaks, finding the cause becomes much harder.

**Important:** More addons do not always mean better performance or compatibility. Two addons may modify the same gameplay systems, use incompatible scripts, or require dependencies that are missing.

---

# PART 3: What to Do If You Make a Mistake

Do not panic if the addon does not work. Most installation problems can be investigated by checking the folders, registration files, and server logs.

## Problem 1: I Extracted the Addon, but I Still See a `.mcpack` File

**What happened:** The `.mcaddon` contained one or more `.mcpack` files, so you have only completed the first extraction.

**How to fix it:**

1. Select the `.mcpack` file.
2. Choose Extract, Unarchive, or Unzip.
3. Open the extracted contents.
4. Repeat if you find another archive.
5. Stop extracting when you reach the actual pack folder containing `manifest.json`.
6. Put that folder into the correct pack directory.

Do not simply rename `.mcpack` to `.zip` unless your extraction tool specifically requires a compatible archive extension. Renaming alone does not extract the files.

## Problem 2: I Cannot Find `manifest.json`

Check the following:

1. Open the folder you extracted.
2. Check whether you are still inside an outer folder.
3. Look for another `.mcpack` or archive file and extract it if necessary.
4. Search inside the extracted folders for `manifest.json`.

If the file still does not exist, the addon may be incomplete, incorrectly packaged, or not a standard Behavior Pack or Resource Pack.

Do not invent a UUID or version to replace the missing manifest.

## Problem 3: I Put the Addon in the Wrong Folder

For example, you accidentally put a Resource Pack inside `behavior_packs`.

**How to fix it:**

1. Stop the server.
2. Move the actual pack folder to the correct directory.
3. Check its `manifest.json` to identify the pack.
4. Make sure it is registered in the correct JSON file.
5. Save your changes.
6. Start the server and test again.

Keep Resource Packs in `resource_packs` and Behavior Packs in `behavior_packs`.

## Problem 4: The Server Starts, but the Addon Does Not Work

Check these items one by one:

- Did you install the actual pack folder instead of leaving it as a `.mcpack` archive?
- Does the pack folder contain `manifest.json`?
- Is the pack in the correct directory?
- Did you register it in the correct JSON file?
- Did you copy the correct UUID and version from the pack's `header`?
- Does the addon require both a Behavior Pack and a Resource Pack?
- Does the addon support your server's Minecraft version?
- Does it require other packs, experimental features, or script support?

Fix any problems you find, restart the server, and test again.

## Problem 5: The Server Will Not Start After I Edited the JSON File

The JSON file might have a syntax error.

Common mistakes include:

- Missing commas.
- Extra commas after the last entry.
- Missing quotation marks.
- Missing braces or square brackets.
- Incorrect filenames or file locations.
- Accidentally pasting two separate JSON arrays into one file.

**How to fix it:**

1. Stop the server if it is running.
2. Open the JSON file you edited most recently.
3. Compare its structure with the examples in this guide.
4. Correct any mistakes.
5. Save the file.
6. Start the server again.

If you are unsure what changed, restore the backup you created before installing the addon.

Do not delete the world or reset the server just because a JSON file has an error.

## Problem 6: The Addon Worked Before, but It Broke After I Added Another Addon

The new addon may conflict with an existing addon, use incompatible dependencies, or introduce a problem during loading.

**How to troubleshoot it:**

1. Stop the server.
2. Back up the current files.
3. Find the most recently installed addon.
4. Remove only that addon's entries from the relevant JSON registration files.
5. Leave the other packs and their entries in place.
6. Save the files and restart the server.
7. Check whether the other addons work again.

If everything works after removing the newest addon's entries, investigate that addon before reinstalling it.

Do not immediately delete all your addons or your world.

## Problem 7: The Textures, Models, or Sounds Are Missing

The Resource Pack may not have been installed or registered correctly.

Check that:

1. The Resource Pack folder is inside `resource_packs`.
2. It contains its own `manifest.json`.
3. Its UUID and version match its manifest.
4. It has an entry in `world_resource_packs.json`.
5. The addon version is compatible with your Minecraft server version.

Some Resource Packs depend on matching Behavior Packs. If your addon includes both, verify that both are installed.

## Problem 8: The Addon Is Installed, but Its Commands or Features Do Not Work

Installing a pack does not automatically guarantee that every feature will work.

Possible causes include:

- The addon requires another pack.
- The addon needs a particular Minecraft version.
- The addon uses unsupported scripts or server features.
- Experimental features are required.
- The addon was designed for single-player rather than a dedicated server.
- Another addon conflicts with it.

Read the original addon's installation instructions and check the server console or logs for errors.

Do not randomly change manifest UUIDs or versions to try to fix the issue.

## Problem 9: I Accidentally Deleted an Existing JSON Entry

If you have a backup, restore the original registration file.

If you do not have a backup:

1. Stop the server.
2. Check which packs are installed in the world.
3. Open each pack's `manifest.json`.
4. Identify the correct UUID and version for each pack.
5. Rebuild the registration file using the packs you want to keep.
6. Validate the JSON syntax.
7. Restart and test the server.

Be careful: if you are unsure which packs belong to the world, do not guess. Ask your server administrator for help or restore a known-good backup.

## Problem 10: I Want to Remove an Addon

You do not need to delete the whole world.

1. Stop the server.
2. Back up the current files.
3. Open `world_behavior_packs.json` and remove the entry for the unwanted Behavior Pack.
4. Open `world_resource_packs.json` and remove the entry for the unwanted Resource Pack, if applicable.
5. Save both JSON files.
6. Restart and test the server.

After confirming the addon is no longer needed, you can remove its pack folder as well.

Do not remove an entry if you are unsure whether another addon depends on that pack.

---

# PART 4: Best Practices for Installing Multiple Addons

Follow these recommendations to reduce installation errors.

### 1. Install One Addon at a Time

Install one addon, register it, restart the server, and test it before proceeding to the next.

This makes troubleshooting easier.

### 2. Never Merge Different Pack Folders

Keep different packs separate, even when they come from the same `.mcaddon`.

For example:

```text
behavior_packs/
├── Economy_BP/
├── Furniture_BP/
└── Mobs_BP/
```

Do not combine all three folders into one folder.

### 3. Keep Existing JSON Entries

When adding another pack, append a new entry to the existing array.

Do not replace the whole file unless you intend to rebuild the registration list.

### 4. Do Not Guess UUIDs or Versions

Every pack must be registered with the correct UUID and version from its own manifest.

Incorrect values can prevent the intended pack from being loaded.

### 5. Watch for Dependencies

Some addons need another Behavior Pack, Resource Pack, or supported script module.

If your addon package includes additional required packs, install those too. Read its official instructions to determine what is required.

### 6. Keep Backups

Before installing a large addon or making significant changes:

- Back up the world.
- Back up `world_behavior_packs.json`.
- Back up `world_resource_packs.json`.

Store the backups somewhere separate from the files you are editing.

### 7. Avoid Installing Too Many Addons at Once

Install a small number at a time and test their features before adding more.

The best number of addons depends on compatibility, server resources, scripts, and what each addon does.

---

# PART 5: Quick Reference

## Folder Locations

```text
Active World/
├── behavior_packs/
│   ├── Addon1_BP/
│   └── Addon2_BP/
│
├── resource_packs/
│   ├── Addon1_RP/
│   └── Addon2_RP/
│
├── world_behavior_packs.json
└── world_resource_packs.json
```

This is an example. Add only the pack types that each addon actually includes.

## Registration Files

```text
world_behavior_packs.json
```

Contains the UUID and version of every Behavior Pack registered to the world.

```text
world_resource_packs.json
```

Contains the UUID and version of every Resource Pack registered to the world.

## Where to Find the Values

```text
Behavior Pack:
behavior_packs → YourPack → manifest.json → header

Resource Pack:
resource_packs → YourPack → manifest.json → header
```

Copy:

```text
header.uuid
header.version
```

Do not copy the module UUID by mistake.

## The Most Important Rules

1. Stop the server before editing files.
2. Back up the world and registration files.
3. Extract `.mcaddon` files completely.
4. If extraction produces `.mcpack` files, extract those too.
5. Stop when you reach the actual pack folder containing `manifest.json`.
6. Put each Behavior Pack in `behavior_packs`.
7. Put each Resource Pack in `resource_packs`.
8. Register every pack in the correct existing JSON file.
9. Never overwrite other addon entries accidentally.
10. Restart the server and test after saving.

If something breaks, stop and check the last change you made. Restore your backup if necessary, and avoid deleting the world as a first troubleshooting step.

## Official References

- [Getting Started with Bedrock Dedicated Server - Microsoft Learn](https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/getting-started?view=minecraft-bedrock-stable)
- [Add-Ons Reference: manifest.json - Microsoft Learn](https://learn.microsoft.com/en-us/minecraft/creator/reference/content/addonsreference/packmanifest?view=minecraft-bedrock-stable)

## Video Guide

https://drive.google.com/file/d/12-Od4b0fmyAHJEK4_sGzR3L9wsXNh6mZ/view?usp=drivesdk
