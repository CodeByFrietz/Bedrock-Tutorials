# Minecraft Bedrock Experimental Features and World Upload Guide for BaoHost

**Minecraft Bedrock Edition | Experimental Features | World Export | BaoHost | Bedrock Dedicated Server | Paper Crossplay**

This guide explains how to enable experimental features in Minecraft Bedrock Edition, export or download a world from Minecraft, prepare the world file, and upload it to a BaoHost server.

It covers two different server types:

1. **BaoHost Bedrock Server:** Upload a Bedrock world directly to a compatible Minecraft Bedrock server.
2. **BaoHost Paper Server:** Convert a Bedrock world into Java Edition format before uploading it to a Paper server.

The guide also explains how to enable Beta APIs, preserve world files, install the required behavior packs and resource packs, configure the correct world name, and troubleshoot common problems.

> **Important:** Minecraft worlds can be damaged or become incompatible after changes to experimental features. Always make a backup before changing experiments, converting a world, or replacing a server world.

---

# Table of Contents

- [1. Understanding Experimental Features](#1-understanding-experimental-features)
- [2. Requirements](#2-requirements)
- [3. Choose Your BaoHost Server Type](#3-choose-your-baohost-server-type)
- [4. Enable Experimental Features in Minecraft Bedrock](#4-enable-experimental-features-in-minecraft-bedrock)
- [5. Enable Beta APIs and Other Required Experiments](#5-enable-beta-apis-and-other-required-experiments)
- [6. Check That the World Has Experiments Enabled](#6-check-that-the-world-has-experiments-enabled)
- [7. Export or Download Your Minecraft World](#7-export-or-download-your-minecraft-world)
- [8. Prepare the World File for Upload](#8-prepare-the-world-file-for-upload)
- [9. Upload a Bedrock World to BaoHost Bedrock](#9-upload-a-bedrock-world-to-baohost-bedrock)
- [10. Configure the Active Bedrock World](#10-configure-the-active-bedrock-world)
- [11. Upload a Bedrock World to BaoHost Paper](#11-upload-a-bedrock-world-to-baohost-paper)
- [12. Install Required Behavior Packs and Resource Packs](#12-install-required-behavior-packs-and-resource-packs)
- [13. Start and Test the Server](#13-start-and-test-the-server)
- [14. Troubleshooting](#14-troubleshooting)
- [15. Frequently Asked Questions](#15-frequently-asked-questions)
- [16. Final Checklist](#16-final-checklist)
- [17. Official Downloads and Documentation](#17-official-downloads-and-documentation)

---

# 1. Understanding Experimental Features

Minecraft Bedrock Edition includes experimental features that allow players and creators to test functionality that is still being developed.

Depending on your Minecraft version, available experiments may include features for:

- Upcoming gameplay changes.
- Creator features.
- Custom blocks or biomes.
- Beta APIs.
- Script-enabled behavior packs.
- Other features still under development.

The names and availability of these options can change between Minecraft releases.

## What are experimental features?

Experimental features are world settings that enable certain features that are not part of the standard gameplay configuration for that world.

They are enabled on the world itself, not simply by changing the server's network settings.

For example, if you created a Bedrock world on your computer and enabled Beta APIs, the world can carry that experimental configuration when exported and uploaded to a compatible Bedrock server.

**Important:** Experimental features can introduce bugs, crashes, or compatibility problems. A world that uses experiments may not work correctly after a Minecraft update.

Minecraft's official documentation also explains that an existing world is copied when experiments are enabled, and that a world with experimental features cannot be returned to a non-experimental state through the normal world settings.

Official documentation:

https://feedback.minecraft.net/hc/en-us/articles/4403610710797-Experimental-Features-Toggle-in-Minecraft-Bedrock-Edition

## Why do I need to enable experiments before uploading?

BaoHost's instructions explain that Beta APIs and experimental features must be enabled on the world before uploading it to the server.

They cannot simply be enabled by adding a normal setting to the server's configuration files.

The recommended process is:

1. Open Minecraft Bedrock Edition.
2. Enable the experiments required by the world.
3. Save the world.
4. Export or download the correct world copy.
5. Upload it to BaoHost.
6. Install any required behavior packs or resource packs.
7. Start and test the server.

BaoHost documentation:

https://help.baohost.com/articles/bedrock-beta-apis

---

# 2. Requirements

Before starting, prepare the following.

## Required

- Minecraft Bedrock Edition.
- Access to the world you want to upload.
- Access to your BaoHost panel.
- Permission to upload files.
- Permission to stop and restart your server.
- Enough storage to hold the exported world.
- A backup of the original world.

## Recommended

- A computer for managing the exported world files.
- A ZIP utility if your device cannot prepare the required archive.
- The relevant behavior packs and resource packs, if your world uses them.
- Access to the BaoHost server console.
- The Minecraft version that created the world.

## If you want to upload to a Bedrock server

You need a BaoHost Bedrock server that supports the world's version and any features or packs the world requires.

The world can generally be imported directly without converting its format.

## If you want to upload to a Paper server

You need a compatible Paper server and a world conversion tool.

A Bedrock world cannot normally be uploaded directly into a Java Paper server and expected to load correctly.

You need to convert the world into Java Edition format first.

This conversion can lose some information, particularly entities, player inventories, experimental features, or content provided by Bedrock add-ons.

Do not assume every Bedrock feature will be preserved.

---

# 3. Choose Your BaoHost Server Type

Before uploading anything, determine which kind of server you have.

This is important because Bedrock and Java worlds use different storage formats.

## Option A: BaoHost Bedrock Server

Choose this path if your goal is to run the world as a Minecraft Bedrock server.

The general process is:

```text
Minecraft Bedrock World
          |
          v
Enable Required Experiments
          |
          v
Export the World
          |
          v
Prepare the World Archive
          |
          v
Upload to BaoHost Bedrock
          |
          v
Extract into the worlds Directory
          |
          v
Configure level-name
          |
          v
Start and Test
```

The original Bedrock world format is retained.

## Option B: BaoHost Paper Server

Choose this path if your goal is to run a Java Edition server that supports Bedrock players through a compatible crossplay setup.

The process is:

```text
Minecraft Bedrock World
          |
          v
Enable Required Experiments
          |
          v
Export the World
          |
          v
Convert Bedrock to Java Format
          |
          v
Upload to BaoHost Paper
          |
          v
Import Using World Manager
          |
          v
Start and Test
```

A conversion tool such as Chunker can convert many world components between Bedrock and Java formats, but it does not preserve every type of data.

Official conversion documentation:

https://learn.microsoft.com/en-us/minecraft/creator/documents/chunkeroverview

## Which option should I use?

| Your goal | Correct option |
|---|---|
| Host the world as a Bedrock server | BaoHost Bedrock |
| Keep the world in Bedrock format | BaoHost Bedrock |
| Host a Java world with Paper | BaoHost Paper |
| Let Java and Bedrock players join a Paper server | Convert the Bedrock world first, then configure compatible crossplay |
| Preserve every experimental feature from a Bedrock world in Paper | Not guaranteed; some features cannot be converted |

---

# 4. Enable Experimental Features in Minecraft Bedrock

This section explains how to enable experiments on your local Minecraft Bedrock world.

The exact names of the options may differ depending on your Minecraft version and platform.

## Step 1: Open Minecraft Bedrock Edition

Start Minecraft Bedrock Edition on the device where your world is saved.

## Step 2: Open the Worlds menu

Select **Play**.

Locate the world you want to use.

## Step 3: Open the world settings

Select the pencil or Edit button next to the world.

Do not immediately enter the world. Open its settings first.

## Step 4: Back up the world

If the world contains important builds or progress, create a separate copy before enabling experimental features.

This is strongly recommended because experiments are not guaranteed to be stable.

If the world is especially important, keep an untouched original and perform the changes on a copy.

## Step 5: Open the Game settings

Within the world settings, open the Game section.

Scroll down until you find the Experiments section.

## Step 6: Find the experiments you need

Depending on your version and add-ons, you may see options with names such as:

- Beta APIs.
- Vanilla Experiments.
- Upcoming Creator Features.
- Other experimental toggles.

Enable only the experiments required by your world or add-ons.

Do not automatically enable every experiment. Each option has a particular purpose, and not every world needs all of them.

## Step 7: Confirm the warning

Minecraft may display a warning asking whether you want to activate experimental gameplay.

Read the message and select the confirmation option if you want to continue.

Experimental features can cause a world to crash, become incompatible with future updates, or behave differently from a normal world.

## Step 8: Check the resulting world

When experiments are enabled on an existing world, Minecraft automatically creates a copy with a name similar to:

```text
Copy of My World
```

The exact name depends on the original world.

Locate the newly created copy in the Worlds menu.

**Use this experimental copy for the next steps, not the untouched original.**

## Step 9: Save and exit

Open the experimental copy and verify that it loads.

After checking it, exit the world normally.

You are now ready to export the correct world.

Official instructions:

https://feedback.minecraft.net/hc/en-us/articles/4403610710797-Experimental-Features-Toggle-in-Minecraft-Bedrock-Edition

---

# 5. Enable Beta APIs and Other Required Experiments

Some Minecraft Bedrock add-ons use Beta APIs or other experimental features.

These features must be enabled on the local world when required.

## Step 1: Check the add-on requirements

If you are using a behavior pack, script pack, or creator add-on, read its installation instructions.

The creator should specify which experimental features are required.

Not all add-ons use Beta APIs.

## Step 2: Open the experimental world settings

Return to the Worlds menu.

Select Edit for the experimental world copy.

Open the Game settings and locate Experiments.

## Step 3: Enable Beta APIs if required

If the world or add-on requires Beta APIs and that option is available in your version, enable it.

If the option is not present, do not assume that another experiment is a direct replacement.

Check whether the add-on supports your Minecraft version and whether the setting has been renamed, removed, or changed.

## Step 4: Enable other required toggles

Enable any additional experiments specified by the add-on's documentation.

Different add-ons can require different combinations.

## Step 5: Save and test the world

Return to the world and test that the add-on works.

Look for missing blocks, missing items, error messages, or other signs that the required features are not available.

If the world already depends on a behavior pack, make sure that the pack itself is enabled.

## Step 6: Export only after confirming the settings

After the world loads and the required features work, proceed to exporting it.

The objective is to export the world that already contains the required experimental settings.

## Important warning

Enabling Beta APIs or other experiments is not a substitute for installing the actual behavior pack, resource pack, or script files.

Those files may also be needed on the server.

---

# 6. Check That the World Has Experiments Enabled

Before downloading the world, confirm that you have selected the correct copy.

## Step 1: Return to the Worlds list

Look for your experimental world.

Depending on the version, it may have an Experimental label next to the game mode.

## Step 2: Open its settings

Select Edit and open Game settings.

Scroll down to the Experiments section.

## Step 3: Confirm the selected toggles

Check that the experiments you need are enabled.

If your world depends on Beta APIs, confirm that the relevant option is enabled where required and available.

## Step 4: Confirm that you selected the copied world

If you enabled experiments on an existing world, make sure you are preparing the new experimental copy.

Do not accidentally export the original, unmodified world.

## Step 5: Keep the original backup

Do not delete the original world.

Keep it until the uploaded server world has been tested and confirmed to work.

Official documentation:

https://feedback.minecraft.net/hc/en-us/articles/4403610710797-Experimental-Features-Toggle-in-Minecraft-Bedrock-Edition

---

# 7. Export or Download Your Minecraft World

The exact export method depends on the device where your world is saved.

When supported, Minecraft Bedrock can export a world as a `.mcworld` file.

This is usually the simplest way to transfer a world.

## 7.1. Export from Minecraft Bedrock on Windows

### Step 1: Open Minecraft Bedrock Edition

Start the game on Windows.

### Step 2: Open the Worlds menu

Select Play and locate the experimental world copy.

### Step 3: Open Edit

Select the pencil or Edit button beside the world.

### Step 4: Locate Export World

Look for the **Export World** button in the world settings.

Its location may vary depending on the Minecraft version.

### Step 5: Export the world

Select Export World.

Choose a location on your computer where you want to save the world.

For example:

```text
Documents/
└── MinecraftWorldBackups/
    └── MyExperimentalWorld.mcworld
```

This is an example folder arrangement. Your actual file location may differ.

### Step 6: Wait until the export finishes

Do not close Minecraft while the export is still running.

After the export completes, check that the `.mcworld` file exists.

### Step 7: Keep a backup

Make another copy of the exported file and store it somewhere safe.

You will use a copy for the server upload.

---

## 7.2. Export from Minecraft Bedrock on Android or iOS

The exact steps depend on the device and the features available in your version of Minecraft.

### Step 1: Open Minecraft

Start Minecraft Bedrock Edition.

### Step 2: Locate the experimental world

Select Play and find your world copy.

### Step 3: Open its settings

Select Edit and look for the world export option, if available.

### Step 4: Export or share the world

If the export feature is available, save the `.mcworld` file to your device storage or a location accessible through your file manager.

On some devices, the file may be saved through the system's sharing interface.

### Step 5: Verify the export

Make sure the exported file is available in your file manager.

Transfer a copy to your computer if that makes preparing and uploading the archive easier.

### What if the Export World option is missing?

Some platforms and versions do not provide the same export interface.

In that situation, use a supported method to access or transfer the world folder from the device, if available.

Do not delete the original world or modify its internal files without making a backup.

---

## 7.3. Export from a console

Xbox, PlayStation, and Nintendo Switch do not necessarily provide the same direct world-export functionality as Windows.

If your console does not provide a world export option, you may need a supported transfer method, such as using a compatible Realms workflow or moving the world to a platform where it can be exported.

The exact method depends on the console and your Minecraft version.

Do not assume you can access the console's Minecraft world directory directly.

---

## 7.4. What file should I have?

If the world was exported successfully, you will commonly have a file similar to:

```text
MyExperimentalWorld.mcworld
```

This is the packaged Bedrock world.

You do not normally need to extract it manually before using Minecraft's import function.

However, BaoHost's file manager may require the world to be uploaded as a `.zip` archive.

The next section explains how to prepare the file.

---

# 8. Prepare the World File for Upload

BaoHost's instructions explain that an exported `.mcworld` file can be renamed to `.zip` when preparing it for the server panel.

A `.mcworld` file is already a packaged archive, so this is a file-extension change, not an additional compression step.

Always keep an untouched copy of the original export.

## Option A: You have a `.mcworld` file

For example:

```text
MyExperimentalWorld.mcworld
```

### Step 1: Make a copy

Create a duplicate of the exported world file.

Keep the original `.mcworld` file as a backup.

### Step 2: Change the file extension

Rename the copy to:

```text
MyExperimentalWorld.zip
```

Do not change or delete the actual world data.

### Step 3: Check the extension carefully

Windows may hide known file extensions.

Make sure you do not accidentally create a file named:

```text
MyExperimentalWorld.mcworld.zip.mcworld
```

or:

```text
MyExperimentalWorld.zip.zip
```

The file should end in `.zip`.

### Step 4: Check the file

Confirm that the archive exists and has a plausible file size.

A successful rename does not guarantee that the world is complete, so keep the original export available.

---

## Option B: You have a world folder instead

If you accessed the world folder directly rather than exporting a `.mcworld` file, you need to compress the entire folder.

The folder contains the world database and related metadata.

A Bedrock world might look similar to:

```text
MyExperimentalWorld/
├── level.dat
├── levelname.txt
├── db/
├── world_behavior_packs.json
├── world_resource_packs.json
├── behavior_packs/
└── resource_packs/
```

The exact files depend on the world and its installed packs.

### Step 1: Locate the root world folder

Find the folder that contains the world's `level.dat` file.

### Step 2: Keep the entire folder

Do not select only `level.dat`.

Do not upload only the `db` folder.

The world needs its database and associated files.

### Step 3: Compress the entire folder

Create a ZIP archive that contains the world folder.

The correct structure should look like:

```text
MyExperimentalWorld.zip
└── MyExperimentalWorld/
    ├── level.dat
    ├── levelname.txt
    ├── db/
    └── ...
```

The archive should contain the actual world folder and its contents.

### Incorrect structure

Do not create an incomplete archive containing only selected files.

Also avoid an unnecessary extra wrapper folder that makes the final extracted structure look like:

```text
worlds/
└── MyExperimentalWorld/
    └── MyExperimentalWorld/
        ├── level.dat
        └── db/
```

If the folder is nested twice, the server may not load the world from the expected location.

---

# 9. Upload a Bedrock World to BaoHost Bedrock

Follow this section if your BaoHost server runs Minecraft Bedrock Dedicated Server.

You can upload the Bedrock world without converting it to Java format.

## Step 1: Back up the server's current world

Before replacing the active world, create a backup through BaoHost if available.

Do not assume that the downloaded local world is also a backup of the current server world.

## Step 2: Stop the Bedrock server

Open the BaoHost panel.

Stop the server and wait for it to shut down fully.

Do not upload or replace the active world while the server is running.

## Step 3: Open the Files section

Open the Files or File Manager tab in BaoHost.

Locate the server's `worlds` directory.

A standard Bedrock Dedicated Server structure looks like:

```text
server/
├── server.properties
├── worlds/
├── behavior_packs/
└── resource_packs/
```

The exact files depend on your server installation.

## Step 4: Open `worlds/`

Open:

```text
worlds/
```

For the standard Bedrock Dedicated Server directory layout, active world folders belong inside this directory.

BaoHost's general world-import instructions also direct users to upload Bedrock world archives into the `worlds/` folder.

Official BaoHost guide:

https://help.baohost.com/articles/import-export-worlds

## Step 5: Upload the prepared archive

Upload the prepared `.zip` archive to the `worlds/` directory.

For example:

```text
worlds/
└── MyExperimentalWorld.zip
```

Wait until the upload reaches 100%.

Do not restart the server during the upload.

## Step 6: Extract the archive

Select the uploaded file in the file manager.

Choose Extract, Unarchive, or the equivalent option available in your panel.

After extraction, make sure the result contains the actual world folder.

The final structure should resemble:

```text
worlds/
└── MyExperimentalWorld/
    ├── level.dat
    ├── levelname.txt
    ├── db/
    └── ...
```

The extracted world folder needs to be directly inside `worlds/`.

If there is an extra wrapper directory, move or extract the actual world folder so the structure is correct.

## Step 7: Confirm the world name

Record the exact folder name.

For example:

```text
MyExperimentalWorld
```

You will need this name when configuring the active world.

## Step 8: Continue to Section 10

You must configure the server to load the correct world folder.

Simply uploading the world does not always cause the server to select it automatically.

---

# 10. Configure the Active Bedrock World

Bedrock Dedicated Server uses the `level-name` setting in `server.properties` to identify the world that should load.

The name must match the world folder under `worlds/`.

## Step 1: Open `server.properties`

In the BaoHost file manager, find:

```text
server.properties
```

Open the file using the panel's editor.

## Step 2: Find `level-name`

Look for a line similar to:

```properties
level-name=Bedrock level
```

The value depends on your current server configuration.

## Step 3: Change the value to your uploaded world folder name

If your uploaded folder is:

```text
worlds/MyExperimentalWorld/
```

set:

```properties
level-name=MyExperimentalWorld
```

The name must match the folder name exactly, including capitalization and spaces.

For example, `MyExperimentalWorld` is different from `myexperimentalworld` on systems that distinguish letter case.

Avoid unusual characters in world folder names where possible.

## Step 4: Save the file

Save `server.properties`.

Make sure you did not accidentally change other settings.

## Step 5: Check for required behavior packs and resource packs

If the world uses add-ons, continue to Section 12 before testing.

The world might load without all its content if required pack files are missing.

## Step 6: Start the server

Start your Bedrock server.

Check the console for world-loading errors.

## Step 7: Test the world

Join the server from a compatible Bedrock client.

Confirm that your builds, world layout, settings, and required experimental features are working.

Official Microsoft documentation:

https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/getting-started

Bedrock server properties:

https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/server-properties

## BaoHost file-placement note

BaoHost's experiment-specific article describes uploading the archive to the server root and extracting it there, while its general Bedrock world-import article directs users to `worlds/`.

For a standard Bedrock Dedicated Server, the active world folder belongs under `worlds/`.

If your panel uses a different layout or the BaoHost-specific instructions for your installation differ, verify where the actual active world folder belongs before deleting or moving anything.

The final structure and `level-name` must be consistent with your server's configuration.

---

# 11. Upload a Bedrock World to BaoHost Paper

This section is for users running a Java Edition server with Paper.

**A Bedrock world cannot simply be uploaded directly into Paper and expected to work.**

Bedrock and Java use different world-storage formats.

You need to convert the world before uploading it to Paper.

## What tool should I use?

Chunker is a world conversion tool that supports converting worlds between Minecraft Bedrock Edition and Java Edition.

Official project releases:

https://github.com/HiveGamesOSS/Chunker/releases

Microsoft's Chunker overview:

https://learn.microsoft.com/en-us/minecraft/creator/documents/chunkeroverview

Chunker is developed by third-party contributors. Use it at your own discretion and keep a backup of the source world.

## Step 1: Export the Bedrock world

Complete Sections 4–8 first.

You should have a copy of the Bedrock world exported as a `.mcworld` file or prepared archive.

Do not use your only copy for conversion.

## Step 2: Download Chunker

Open:

https://github.com/HiveGamesOSS/Chunker/releases

Download the application version suitable for your operating system.

Follow the instructions included with the release.

## Step 3: Open Chunker

Launch the application.

Use the world selection screen to select your Bedrock world.

Chunker supports importing a world from a folder or a supported archive, including a `.mcworld` file.

If your exported file has been renamed to `.zip`, you can select that archive instead.

## Step 4: Select the Bedrock source world

Choose the Bedrock world you exported.

Verify that you selected the experimental copy rather than the original.

## Step 5: Select Java Edition as the output

When Chunker asks for the output format, select Minecraft Java Edition.

Choose an output version compatible with your target Paper server.

Do not select a Java version that the server cannot run.

## Step 6: Review the conversion options

Review the available options before converting.

Some world content may not be supported by the conversion process.

Chunker can convert many world components, including:

- Level settings.
- Blocks and biomes.
- Tile entities.
- Multiple dimensions.
- Containers and items.
- In-game maps.

However, its documented conversion limitations include entities and player inventories.

Experimental content and add-ons require additional care. Custom Bedrock blocks, behaviors, scripts, and other experimental features may not have Java equivalents.

Do not assume that all experimental features will work after converting the world.

## Step 7: Convert the world

Start the conversion.

Wait until it finishes.

If the application reports an error or an unsupported feature, review the message before uploading the output.

## Step 8: Export or download the converted world

Save the converted Java world to your computer.

Prepare the output in the archive format required by the BaoHost Java World Manager, typically a ZIP archive for its Select .zip workflow.

Keep both files:

```text
MyExperimentalWorld_Bedrock_Backup.mcworld
MyExperimentalWorld_Java_Converted.zip
```

These are example filenames.

Keep the original Bedrock world even after conversion succeeds.

## Step 9: Stop your BaoHost Paper server

Open the BaoHost panel and stop the server.

Wait until it has shut down fully.

## Step 10: Open World Manager

BaoHost provides a World Manager for Java servers.

Open it from your server panel.

The available actions may vary depending on your server setup.

## Step 11: Choose the correct import mode

BaoHost documents the following modes.

### Replace Mode

Choose Replace Mode if you want the converted world to replace your current Paper world.

The World Manager's documented workflow automatically archives the current world as a backup before replacement.

However, always confirm that you are using the correct server and that the backup was created.

### Add Mode

Choose Add Mode if you want to add another world without replacing the existing one.

This is useful for multi-world configurations.

Adding a folder to a server does not necessarily make it the active world; additional world management may be needed depending on your setup.

### Import via URL

BaoHost also documents an Import via URL option.

Use it only if your converted archive is available at a direct downloadable link and you understand who can access it.

For most beginners, uploading the converted ZIP directly is simpler.

## Step 12: Upload the converted world

For Replace Mode:

1. Select the replacement option.
2. Choose the converted `.zip` archive.
3. Upload the file.
4. Let World Manager finish importing the world.

For Add Mode:

1. Enter a folder name.
2. Select the converted `.zip` archive.
3. Upload the file.
4. Follow the panel's instructions for activating or managing the additional world.

## Step 13: Check the world selection

If you are importing manually rather than using World Manager, open `server.properties` and check:

```properties
level-name=world
```

If the converted folder is named something else, change the folder name or the `level-name` value so the two match.

Do not change this setting unnecessarily if World Manager handles the installation and the server already loads the correct world.

## Step 14: Start the Paper server

Start the server.

Check the console for errors related to:

- World loading.
- Invalid or unsupported world data.
- Missing plugins.
- Missing resource packs.
- Unsupported blocks or content.

## Step 15: Test the converted world

Join the server using Java Edition.

Check:

- Your builds.
- Terrain and biomes.
- Chests and containers.
- The Nether and End, if included.
- Spawn location.
- Any converted gameplay settings.

If you plan to use Bedrock crossplay, test with a Bedrock client after confirming that the Java world loads correctly.

**Important:** Converting to Java format does not automatically turn Bedrock experimental features into Java features. Some content may be lost or behave differently.

---

# 12. Install Required Behavior Packs and Resource Packs

Uploading a world folder does not guarantee that every required add-on is available on the server.

Some Bedrock worlds depend on behavior packs or resource packs.

## What is a behavior pack?

A behavior pack can add or modify gameplay behavior, such as entity behavior, recipes, items, scripts, or other supported mechanics.

## What is a resource pack?

A resource pack can provide textures, models, sounds, and other supported visual or audio content.

Some worlds require both.

## Step 1: Check the world folder

Look for files such as:

```text
world_behavior_packs.json
world_resource_packs.json
```

These files can identify packs that the world expects to use.

Their presence does not guarantee that every required pack is installed.

## Step 2: Check the exported world

If the world uses add-ons, make sure you have the corresponding pack files.

Do not assume the world export automatically contains every required add-on that was installed separately on your device.

## Step 3: Install the packs on a Bedrock server

For Bedrock Dedicated Server, behavior packs and resource packs may be installed in folders that are specific to the world or shared across the server.

A typical server structure includes:

```text
server/
├── worlds/
│   └── MyExperimentalWorld/
│       ├── level.dat
│       ├── db/
│       ├── behavior_packs/
│       └── resource_packs/
├── behavior_packs/
└── resource_packs/
```

The exact pack installation method depends on the pack and server configuration.

World-specific packs belong with the relevant world when the pack is installed that way.

Shared packs can be installed in the server-level `behavior_packs` or `resource_packs` directories when appropriate.

Follow the pack creator's instructions.

Official Microsoft server documentation:

https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/getting-started

## Step 4: Check pack identifiers and versions

If the world references a pack by UUID or version, confirm that the installed pack matches the reference.

A missing or mismatched pack can cause content to disappear or fail to load.

## Step 5: Test the world again

Restart the server after installing the required packs.

Join the world and check that the relevant content works.

## What if the destination is Paper?

Bedrock behavior packs and resource packs are not directly compatible with Paper.

Java Edition uses different plugin, data pack, and resource pack systems.

A converted world may preserve some basic world content while losing functionality supplied by Bedrock-specific add-ons.

You must find an equivalent Java plugin, data pack, resource pack, or mod if one exists and is compatible with your server.

Do not upload Bedrock behavior packs into Paper's `plugins` folder and expect them to work.

---

# 13. Start and Test the Server

After uploading the world and configuring the relevant settings, perform a complete test.

## Step 1: Start the server

Use the BaoHost panel to start the server.

Wait until the console shows that the server has finished loading.

## Step 2: Check the logs

Look for errors related to:

- Missing world files.
- Invalid world paths.
- Unsupported world data.
- Experimental features.
- Missing behavior packs.
- Missing resource packs.
- Incorrect `level-name`.
- Conversion problems.

## Step 3: Join the server

For a Bedrock server, join using Minecraft Bedrock Edition.

For a Paper server, use Java Edition to test the converted Java world.

If your Paper server is configured for crossplay, you can test from Bedrock Edition after confirming the Java server works.

## Step 4: Check your builds

Verify that your important builds and structures are present.

Check different locations in the world rather than only the spawn area.

## Step 5: Check the Nether and End

If the world contains important builds or progress in other dimensions, verify that the relevant dimensions load.

For converted worlds, dimension compatibility depends on the conversion process and output version.

## Step 6: Check packs and experiments

If the world depends on Beta APIs, behavior packs, or experimental content, confirm that the required functionality actually works.

Do not assume that a successful world load guarantees every pack or experimental feature is working.

## Step 7: Make another backup

Once the server is working, create a backup of the uploaded server world.

This gives you a recovery point if a later update causes problems.

---

# 14. Troubleshooting

## Problem 1: The server creates a new world instead of loading the uploaded world

### Possible causes

- The folder is in the wrong directory.
- The `level-name` setting is incorrect.
- The extracted folder contains another nested folder.
- The archive was not extracted correctly.

### Solutions

1. Stop the server.
2. Check the world folder.
3. For Bedrock Dedicated Server, confirm the active world directory is under `worlds/`.
4. Open `server.properties`.
5. Verify that `level-name` matches the folder name exactly.
6. Check for an extra nested folder.
7. Restart the server and test again.

For a Java Paper server, check the server's expected Java world location and the `level-name` setting.

## Problem 2: My world uploads, but the experimental features do not work

### Possible causes

- The wrong world copy was exported.
- The required experiments were not enabled before exporting.
- The server does not support the requested features.
- A required behavior pack is missing.
- An add-on version is incompatible.

### Solutions

1. Open the original local world.
2. Check the experiment settings.
3. Confirm that you exported the experimental world copy.
4. Verify that all required packs are available.
5. Check the server software and Minecraft version.
6. Review the console for missing-pack or feature errors.

If the destination is Paper, remember that Bedrock experimental features do not automatically become Java features.

## Problem 3: I cannot find the exported `.mcworld` file

### Possible causes

- The export was not completed.
- The game saved the file to a different location.
- The operating system opened a share or save dialog instead.
- The platform does not provide the same export function.

### Solutions

1. Repeat the export and check the selected destination.
2. Search your device for the exported world filename.
3. Check your downloads or documents folders.
4. Verify the file extension.
5. Use a supported transfer method if the platform does not offer direct export.

## Problem 4: The server cannot extract my world archive

### Possible causes

- The upload is incomplete.
- The file extension is incorrect.
- The archive is damaged.
- The archive contains an unusual folder structure.

### Solutions

1. Compare the archive size with the original export.
2. Make sure the upload finished.
3. Check the file extension.
4. Recreate the archive from a complete copy of the world.
5. Test the archive locally if possible.
6. Upload it again.

Do not delete the original export.

## Problem 5: My world loads, but my custom items are missing

### Possible causes

- Required behavior packs or resource packs are missing.
- The world references a pack that is not installed on the server.
- The pack version is incompatible.
- The destination server cannot run the relevant feature.

### Solutions

1. Inspect the world's pack references.
2. Install the correct pack files.
3. Check the pack creator's instructions.
4. Confirm the pack version is compatible with the server.
5. Restart and test again.

## Problem 6: The world works locally but crashes on the server

### Possible causes

- The server uses a different Minecraft version.
- The world depends on unsupported experiments.
- A behavior pack is incompatible with the server.
- Required pack files are missing.

### Solutions

1. Restore the latest backup if necessary.
2. Check the server version.
3. Review the console output.
4. Test a copy of the world.
5. Update or remove incompatible packs only after reviewing their documentation.

## Problem 7: My Bedrock world will not load in Paper

This is expected if you upload the original Bedrock world directly to a Java server.

Bedrock and Java use different world formats.

### Solution

1. Keep a backup of the Bedrock world.
2. Open Chunker.
3. Import the Bedrock world.
4. Select Java Edition as the output.
5. Convert the world.
6. Download the converted archive.
7. Import it using BaoHost's Java World Manager.

Official conversion tool:

https://github.com/HiveGamesOSS/Chunker/releases

## Problem 8: Some builds or entities are missing after conversion

World conversion cannot guarantee that every Bedrock feature will be preserved.

Chunker's published documentation lists entities and player inventories among the conversion limitations.

Experimental features, custom content, and add-ons may also be incompatible with Java Edition.

### Solutions

1. Keep the original Bedrock world.
2. Review the conversion tool's current limitations.
3. Check whether the missing content requires an unsupported add-on.
4. Test conversion on a copy.
5. Do not overwrite your original world until you have inspected the output.

---

# 15. Frequently Asked Questions

## Q1. Can I enable experimental features directly in BaoHost?

For the Bedrock experimental toggles covered in this guide, BaoHost's instructions require you to enable them on the local world before uploading it.

Changing ordinary server settings does not automatically enable every world experiment.

## Q2. Do I need to enable experiments before exporting?

Yes, if the world needs those experiments.

Enable the required features on the correct Bedrock world copy, then export that copy.

## Q3. Will the experiment remain enabled after uploading the world?

The uploaded Bedrock world should retain its stored world settings, provided the world is imported correctly and the destination server supports the features.

However, the presence of an enabled experiment does not guarantee that an incompatible server version or missing add-on will support the feature.

## Q4. Can I disable experiments later?

Minecraft's official documentation states that a world using experimental features cannot be restored to a non-experimental state through the normal world settings.

Keep an untouched backup if you may want to return to the original world.

## Q5. Does enabling experiments affect achievements?

Experimental features can affect achievement availability. Check the current warning displayed by Minecraft before enabling them.

If achievements matter to you, keep an untouched copy of your original world.

## Q6. Can I upload the `.mcworld` file directly to BaoHost?

BaoHost's experiment-specific instructions recommend preparing `.mcworld` files as `.zip` files for upload.

Keep the original `.mcworld` file as a backup.

## Q7. Should I upload the world into the `worlds/` directory?

For a standard Bedrock Dedicated Server, the active world folder belongs in `worlds/`.

Make sure its folder name matches the `level-name` property.

## Q8. Can I upload a Bedrock world directly to Paper?

No. A Bedrock world should be converted into Java world format before being imported into Paper.

Use a suitable conversion tool and check its limitations.

## Q9. Will Chunker preserve all my experimental features?

No. Conversion between Minecraft editions is not lossless for all types of content.

Experimental blocks, entities, player inventories, and add-on functionality may not be preserved correctly.

## Q10. Can Java and Bedrock players join the converted world together?

Yes, when the converted world loads correctly on a compatible Java server and the server has a working crossplay setup.

The crossplay bridge does not automatically make Bedrock-only experimental features compatible with Java.

## Q11. What should I do if I use add-ons?

Check the add-on's documentation.

Install the required packs on the Bedrock server. If you are converting to Paper, find compatible Java replacements where available.

## Q12. Should I replace my existing world immediately?

No. Back up the existing server world first.

If possible, test the uploaded world before replacing your main world.

---

# 16. Final Checklist

Use this checklist before considering the setup complete.

## Local Minecraft world

- [ ] The correct Minecraft Bedrock world was selected.
- [ ] A separate backup of the original world exists.
- [ ] The required experimental features are enabled.
- [ ] Beta APIs are enabled if required and available.
- [ ] The correct experimental world copy was selected.
- [ ] The world loads locally.
- [ ] Any required add-ons have been identified.

## World export

- [ ] The world was exported successfully.
- [ ] The `.mcworld` file or complete world folder is saved.
- [ ] The original export has been retained.
- [ ] The upload copy is in an archive format supported by BaoHost.
- [ ] The archive contains the complete world folder.

## BaoHost Bedrock

- [ ] The server was stopped before uploading.
- [ ] The world archive was uploaded.
- [ ] The archive was extracted successfully.
- [ ] The extracted world folder is in the correct location.
- [ ] `level-name` matches the world folder name.
- [ ] Required behavior packs and resource packs are installed.
- [ ] The server starts without relevant errors.
- [ ] The world loads and the required features work.

## BaoHost Paper

- [ ] The original Bedrock world was backed up.
- [ ] The world was converted into Java Edition format.
- [ ] Conversion limitations were reviewed.
- [ ] The converted archive was downloaded.
- [ ] The Paper server was stopped before import.
- [ ] The converted world was imported through World Manager or the manual procedure.
- [ ] The correct world is selected.
- [ ] The server starts without relevant errors.
- [ ] Builds and world content have been checked.
- [ ] Crossplay has been tested if required.

---

# 17. Official Downloads and Documentation

| Resource | Link |
|---|---|
| BaoHost website | https://baohost.com |
| BaoHost Help Center | https://help.baohost.com/ |
| BaoHost Bedrock experimental features guide | https://help.baohost.com/articles/bedrock-beta-apis |
| BaoHost world import/export guide | https://help.baohost.com/articles/import-export-worlds |
| Minecraft Bedrock experimental features documentation | https://feedback.minecraft.net/hc/en-us/articles/4403610710797-Experimental-Features-Toggle-in-Minecraft-Bedrock-Edition |
| Microsoft Bedrock Dedicated Server guide | https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/getting-started |
| Bedrock server properties | https://learn.microsoft.com/en-us/minecraft/creator/documents/bedrockserver/server-properties |
| Chunker overview | https://learn.microsoft.com/en-us/minecraft/creator/documents/chunkeroverview |
| Chunker downloads | https://github.com/HiveGamesOSS/Chunker/releases |

---

# Conclusion

To upload an experimental Minecraft Bedrock world to BaoHost, enable the required experiments on the local world first, export the correct world copy, prepare the archive, and upload it to the appropriate server directory.

For a Bedrock server, keep the world in Bedrock format, place the extracted folder in the correct location, and ensure `level-name` matches the folder name.

For a Paper server, convert the Bedrock world to Java Edition format before importing it. Remember that conversion may not preserve every entity, inventory, experimental feature, or add-on.

Always back up the original world, install required packs, verify compatibility, and test the server before replacing your main world.

**The most important rule is to use the correct world format for your server: Bedrock worlds belong on compatible Bedrock servers, while Paper requires a Java-format world.**
