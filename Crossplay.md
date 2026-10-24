# Complete Minecraft Crossplay Guide for BaoHost

**Minecraft Java Edition + Bedrock Edition | GeyserMC | Floodgate | ViaVersion | ViaBackwards**

This guide explains how to set up a Minecraft Java Edition server on BaoHost that allows both Java and Bedrock players to play together.

It is written for beginners and covers everything from choosing the correct server software to uploading plugins, configuring network ports, testing the connection, and fixing common problems.

You do not need to be an experienced server administrator to follow this guide. However, you should understand what each plugin does and why certain settings are required before changing your server configuration.

> **Important:** Minecraft, GeyserMC, and ViaVersion are regularly updated. The examples in this guide must be checked against your actual server version and the current official documentation. The supported-version information referenced here was checked on October 24, 2026.

---

# Table of Contents

- [1. What Is Minecraft Crossplay?](#1-what-is-minecraft-crossplay)
- [2. How the Crossplay System Works](#2-how-the-crossplay-system-works)
- [3. Requirements Before Starting](#3-requirements-before-starting)
- [4. Understanding the Required Plugins](#4-understanding-the-required-plugins)
- [5. Do You Need ViaVersion and ViaBackwards?](#5-do-you-need-viaversion-and-viabackwards)
- [6. Official Download Links](#6-official-download-links)
- [7. Create or Prepare Your BaoHost Server](#7-create-or-prepare-your-baohost-server)
- [8. What Should You Select in BaoHost?](#8-what-should-you-select-in-baohost)
- [9. Back Up and Stop Your Server](#9-back-up-and-stop-your-server)
- [10. Install GeyserMC and Floodgate](#10-install-geysermc-and-floodgate)
- [11. Install ViaVersion and ViaBackwards](#11-install-viaversion-and-viabackwards)
- [12. Configure GeyserMC](#12-configure-geysermc)
- [13. Configure Floodgate](#13-configure-floodgate)
- [14. Configure BaoHost Network Ports](#14-configure-baohost-network-ports)
- [15. Start the Server and Check the Console](#15-start-the-server-and-check-the-console)
- [16. How Java Players Join](#16-how-java-players-join)
- [17. How Bedrock Players Join](#17-how-bedrock-players-join)
- [18. Console Players: Xbox, PlayStation and Nintendo Switch](#18-console-players-xbox-playstation-and-nintendo-switch)
- [19. Testing That Crossplay Works](#19-testing-that-crossplay-works)
- [20. Troubleshooting](#20-troubleshooting)
- [21. Frequently Asked Questions](#21-frequently-asked-questions)
- [22. Final Setup Checklist](#22-final-setup-checklist)
- [23. Official Documentation and Resources](#23-official-documentation-and-resources)

---

# 1. What Is Minecraft Crossplay?

Minecraft crossplay means players using different platforms or editions can play together on the same server.

Minecraft has two main editions.

## Minecraft Java Edition

Java Edition is primarily available on:

- Windows
- macOS
- Linux

Java players normally connect to Java Edition multiplayer servers.

## Minecraft Bedrock Edition

Bedrock Edition is available on platforms such as:

- Android
- iOS
- Windows Bedrock Edition
- Xbox
- PlayStation
- Nintendo Switch

Bedrock players normally connect to Bedrock multiplayer servers.

## Why can't Java and Bedrock connect directly?

Java Edition and Bedrock Edition use different networking protocols.

A normal Java server does not automatically understand a Bedrock connection. Similarly, a normal Bedrock server does not automatically accept Java Edition clients.

This is where GeyserMC becomes useful.

Geyser allows Bedrock clients to connect to a compatible Java server by translating the communication between the editions.

Floodgate can then allow Bedrock players to authenticate without requiring a separate Java Edition account.

**The goal of this guide is to configure a Java server on BaoHost so compatible Java and Bedrock players can play together in the same world.**

---

# 2. How the Crossplay System Works

The basic connection looks like this:

```text
                BAOHOST SERVER
                       |
             Minecraft Java Server
                       |
          +------------+------------+
          |                         |
          |                         |
   Java Edition Player        GeyserMC
          |                         |
          |                  Bedrock Connection
          |                         |
          |                  Bedrock Player
          |                         |
          +------- SAME WORLD ------+
```

The actual network path is slightly different for Bedrock players:

1. The Bedrock player connects to Geyser's listener.
2. Geyser translates the Bedrock connection into a Java-compatible connection.
3. The connection reaches the Java server.
4. Floodgate handles Bedrock authentication when configured.
5. The Bedrock player enters the same Minecraft world as the Java players.

Java players continue connecting normally to the Java server.

Bedrock players connect through Geyser.

## What each plugin does

| Plugin | Main purpose |
|---|---|
| GeyserMC | Bridges Minecraft Bedrock Edition to a Java server. |
| Floodgate | Allows Bedrock authentication without requiring a separate Java Edition account. |
| ViaVersion | Provides compatibility between supported Minecraft Java protocol versions. |
| ViaBackwards | Allows supported older Java clients to connect to a newer Java server. |

These plugins do different jobs. Installing all of them does not automatically make every edition and version compatible.

---

# 3. Requirements Before Starting

Prepare the following before installing anything.

## Required for the recommended setup

- An active BaoHost Minecraft server.
- Access to the BaoHost game server panel.
- Permission to access the server files.
- Permission to stop and restart the server.
- A compatible Minecraft Java server implementation.
- GeyserMC.
- A suitable network allocation for Geyser.
- The server address or hostname.
- A compatible Minecraft version.

## Strongly recommended

- Floodgate.
- ViaVersion if required by your server version.
- A backup of the server world and configuration.
- Access to the server console.
- A Java player and a Bedrock player available for testing.

ViaBackwards is optional. You only need it if you want to support older Java Edition clients connecting to a newer Java server.

## Do I need to create a new world?

No.

If you already have a compatible server running Paper, Purpur, or Spigot, you can normally install the plugins without creating a new world.

Always create a backup before changing software, installing plugins, or modifying configuration files.

## Do I need a paid Minecraft Java Edition account?

Bedrock players do not need a separate Java Edition account when Floodgate is installed and configured correctly.

They still need a legitimate Minecraft Bedrock installation and any required platform account.

## Do I need a dedicated IP?

Not necessarily.

You need a working server address and a suitable network allocation. BaoHost may assign a shared IP address and a port, or provide another networking arrangement through its panel.

Use the address and port shown in your actual server panel.

---

# 4. Understanding the Required Plugins

Before installing plugins, understand which ones you actually need.

## 4.1. GeyserMC — Required

GeyserMC is the main crossplay component.

It translates Bedrock Edition communication so Bedrock players can connect to a compatible Java server.

Without Geyser or another compatible bridging setup, installing Floodgate alone will not create Java-Bedrock crossplay.

Official website:

https://geysermc.org/

## 4.2. Floodgate — Recommended

Floodgate provides authentication support for Bedrock players.

Without Floodgate, Geyser can be configured to use Java account authentication, but this is a different setup and requires the appropriate Java authentication.

With Floodgate correctly installed, Bedrock players can join without needing a separate Java Edition account.

Official setup guide:

https://geysermc.org/wiki/floodgate/setup/

## 4.3. ViaVersion — Version compatibility

ViaVersion allows supported Minecraft Java clients to connect to supported servers using different Java protocol versions.

It is also important for Geyser compatibility with older Java server versions.

The current Geyser documentation says that Geyser uses a Java client protocol corresponding to Java 26.3. When the Java server does not accept that protocol, ViaVersion may be required.

Check the current requirements here:

https://geysermc.org/wiki/geyser/supported-versions/

Official ViaVersion downloads:

https://hangar.papermc.io/ViaVersion/ViaVersion

## 4.4. ViaBackwards — Optional older-client support

ViaBackwards extends Java protocol compatibility so supported older Java clients can connect to a newer Java server.

ViaBackwards requires ViaVersion.

It is not required merely to allow Bedrock players to join.

Official ViaBackwards downloads:

https://hangar.papermc.io/ViaVersion/ViaBackwards

---

# 5. Do You Need ViaVersion and ViaBackwards?

This is one of the most important parts of the setup.

The short explanation is:

- Geyser provides the Bedrock-to-Java bridge.
- Floodgate handles Bedrock authentication.
- ViaVersion handles Java protocol compatibility.
- ViaBackwards extends Java compatibility toward older clients.

## Recommended plugin combinations

| Your setup | Recommended plugins |
|---|---|
| Java 26.3 server, Bedrock crossplay | GeyserMC + Floodgate |
| Java server on a different version that needs a newer Java protocol | GeyserMC + Floodgate + ViaVersion |
| Newer Java server with support for older Java clients | ViaVersion + ViaBackwards, in addition to any crossplay plugins |
| Bedrock crossplay without a separate Java account | GeyserMC + Floodgate, plus any version compatibility required |
| Older Java clients joining a newer server | ViaVersion + ViaBackwards |
| Java server below 1.20.5 using the current Geyser-Spigot plugin | Do not assume direct installation will work; follow Geyser's documented proxy or alternative setup |

## When is ViaVersion required for Geyser?

As of October 24, 2026, the official Geyser supported-versions page lists Java 26.3 and Bedrock 26.30–26.52 as supported client versions.

It explains that Geyser emulates a Java 26.3 client and that an older Java server needs to accept that protocol.

Therefore, if your backend is not running Java 26.3, check whether ViaVersion is required.

Official source:

https://geysermc.org/wiki/geyser/supported-versions/

The exact supported versions may change. Always check that page before choosing your server version or updating plugins.

## When do I need ViaBackwards?

ViaBackwards is for players who use older Java Edition clients to join a newer server.

For example, you might want your server to run a recent Minecraft version but also allow friends using older Java clients.

In this situation:

1. Install ViaVersion.
2. Install ViaBackwards.
3. Check the supported-version list.
4. Test the older client versions you intend to support.

ViaBackwards cannot make every old client fully identical to the newest client.

Some features, blocks, items, and mechanics may be limited when connecting with older versions.

## Is ViaBackwards required for Bedrock crossplay?

No.

Do not install ViaBackwards just because your server supports Bedrock.

Install it only if you also want supported older Java clients to connect.

## My recommendation

For most BaoHost servers, start by selecting a supported Paper server version, then configure:

```text
GeyserMC
Floodgate
ViaVersion (if required by your server version)
ViaBackwards (optional)
```

Do not install ViaBackwards unless you actually need older Java client support.

---

# 6. Official Download Links

Always download plugins from official project pages.

## GeyserMC

Download:

https://geysermc.org/download

For a Paper, Purpur, or Spigot server, select the Spigot/Paper plugin build.

You normally want the plugin file called something similar to:

```text
Geyser-Spigot.jar
```

The actual filename can vary.

## Floodgate

Download:

https://geysermc.org/download

For a Paper, Purpur, or Spigot server, select Floodgate-Spigot.

The filename may differ between releases.

## ViaVersion

Download:

https://hangar.papermc.io/ViaVersion/ViaVersion

Alternative official sources:

- https://modrinth.com/plugin/viaversion
- https://github.com/ViaVersion/ViaVersion/releases

## ViaBackwards

Download:

https://hangar.papermc.io/ViaVersion/ViaBackwards

Alternative official sources:

- https://modrinth.com/plugin/viabackwards
- https://github.com/ViaVersion/ViaBackwards/releases

## Paper

Download:

https://papermc.io/downloads/paper

## Geyser documentation

Setup:

https://geysermc.org/wiki/geyser/setup/

Supported versions:

https://geysermc.org/wiki/geyser/supported-versions/

Floodgate setup:

https://geysermc.org/wiki/floodgate/setup/

## BaoHost documentation

BaoHost crossplay tutorial:

https://help.baohost.com/articles/geyser-floodgate-crossplay

BaoHost Help Center:

https://help.baohost.com/

---

# 7. Create or Prepare Your BaoHost Server

There are two situations:

1. You are creating a new server.
2. You already have a Minecraft server.

Follow the section that applies to you.

## Situation A: Creating a new server

### Step 1: Open BaoHost

Visit:

https://baohost.com

Log in to your account and open the server management panel.

### Step 2: Create or select your Minecraft server

Open the server creation page, or select your existing Minecraft server if you already created one.

The labels and layout can differ depending on the hosting panel.

### Step 3: Select Minecraft Java Edition

For this guide, select Minecraft Java Edition server software.

Do not select a Bedrock Dedicated Server if you intend to use the plugin-based Java setup described here.

### Step 4: Select Paper

Choose Paper if it is available.

Paper is a good choice because it supports server plugins.

Purpur and Spigot can also be appropriate if supported by the hosting panel.

### Step 5: Select a Minecraft version

Choose a version compatible with the current Geyser release.

For the simplest protocol setup, use a server version that accepts the Java protocol required by the current Geyser build.

As of October 24, 2026, the Geyser documentation lists Java 26.3 as its current supported Java client protocol.

If you choose a different server version, check whether ViaVersion is required.

### Step 6: Select the Java runtime

Use a Java runtime supported by your chosen server software.

The current Geyser setup guide requires Java 21 or newer for Geyser, but a newer Paper release may require a newer Java runtime.

Always follow the requirements of the selected Paper build.

### Step 7: Finish creating the server

Complete the panel's installation process.

Start the server once and confirm that it runs correctly before installing any plugins.

---

## Situation B: You already have a server

If your server already exists, do not create another one unnecessarily.

### Step 1: Open the server panel

Log in to BaoHost.

Select your existing Minecraft server.

### Step 2: Check server software

Look for the software and version shown in your panel.

Examples include:

- Paper
- Purpur
- Spigot
- Vanilla
- Fabric
- Forge
- NeoForge

### Step 3: Check your Minecraft version

Write down the server version.

For the current Geyser-Spigot method, the Geyser setup guide says direct installation requires a Paper/Spigot server running Minecraft 1.20.5 or newer.

If your server runs below 1.20.5, do not assume that adding Geyser-Spigot and ViaVersion will be sufficient. Use the appropriate proxy-based or alternative setup described in the current Geyser documentation.

### Step 4: Continue only when your setup is compatible

If you have compatible plugin-enabled software, continue with this guide.

If you use a modded server, consult the installation instructions for that platform.

---

# 8. What Should You Select in BaoHost?

Use the following as a selection guide when creating your server.

| Setting | Recommended selection |
|---|---|
| Game | Minecraft |
| Edition | Java Edition |
| Server software | Paper |
| Minecraft version | Current version supported by the chosen Geyser release |
| Java runtime | A runtime supported by Paper and Geyser |
| Plugin installation | Enabled through the server's plugins directory |
| Network allocation | A suitable Java server allocation and a compatible Geyser allocation |
| World | Existing world or new world, depending on your preference |

## Why Paper?

Paper supports plugin-based installations of Geyser, Floodgate, ViaVersion, and ViaBackwards.

It is generally a straightforward choice for this setup.

## What if I use Purpur?

Purpur is also a plugin-enabled server implementation.

The same basic installation method can be used if the versions are compatible.

## What if I use Vanilla?

Vanilla does not support Bukkit/Spigot-style plugins.

You cannot simply upload Geyser-Spigot.jar to Vanilla and expect it to work.

Choose compatible plugin-enabled server software or follow a different Geyser installation method.

## What if I use Fabric, Forge, or NeoForge?

These environments use different installation methods.

Do not upload Paper plugins into the `mods` folder.

Consult the Geyser documentation for the appropriate server platform:

https://geysermc.org/wiki/geyser/setup/

---

# 9. Back Up and Stop Your Server

Before uploading anything, make sure you can restore your server if something goes wrong.

## Step 1: Create a backup

Use the backup section of the BaoHost panel if available.

Back up your world and important server configuration files.

## Step 2: Confirm the backup

Make sure the backup completed successfully.

Do not assume a backup exists simply because you clicked the backup button.

## Step 3: Stop the server

Use the Stop button in the BaoHost panel.

Wait until the server completely shuts down.

## Step 4: Open the file manager

Navigate to the Files or File Manager section.

You will normally see folders and files related to your server.

A typical Paper server directory looks like this:

```text
server/
├── plugins/
├── world/
├── server.properties
└── eula.txt
```

The actual file structure can differ.

If the `plugins` folder is missing, verify your server software before proceeding.

---

# 10. Install GeyserMC and Floodgate

This section installs the essential crossplay plugins.

## Step 1: Download GeyserMC

Go to:

https://geysermc.org/download

Select Geyser for Spigot/Paper.

Download the `.jar` plugin file.

## Step 2: Download Floodgate

Use the same download page:

https://geysermc.org/download

Select Floodgate for Spigot/Paper.

Download its `.jar` plugin file.

## Step 3: Open the plugins directory

In the BaoHost file manager, open:

```text
plugins/
```

## Step 4: Upload GeyserMC

Upload the downloaded Geyser `.jar` file into the `plugins` directory.

Wait until the upload finishes.

## Step 5: Upload Floodgate

Upload the Floodgate `.jar` file into the same directory.

The directory might now look like this:

```text
plugins/
├── Geyser-Spigot.jar
└── floodgate-spigot.jar
```

These filenames are examples. Your downloads may use slightly different names.

## Step 6: Start the server

Start the server through BaoHost.

Wait until it finishes loading.

Geyser and Floodgate should generate their configuration files.

## Step 7: Check the generated files

After the initial startup, you may see a directory structure similar to:

```text
plugins/
├── Geyser-Spigot.jar
├── Geyser-Spigot/
│   └── config.yml
├── floodgate-spigot.jar
└── floodgate/
    ├── config.yml
    └── key.pem
```

Names and paths can vary by version.

## Step 8: Stop the server again

Once the configuration files are generated, stop the server before editing them.

## Security warning

Floodgate may generate a file named `key.pem`.

**Never upload this file to a public GitHub repository.**

It is a sensitive authentication key. Do not share it with strangers or include it in public configuration examples.

---

# 11. Install ViaVersion and ViaBackwards

You do not always need these plugins, so determine whether they are necessary before installing them.

## 11.1. Check if ViaVersion is required

Read:

https://geysermc.org/wiki/geyser/supported-versions/

The current Geyser documentation explains which Java protocol the Geyser client emulates.

If your backend server cannot accept that protocol, ViaVersion may be required.

If your server is already running the appropriate Java protocol, you may not need ViaVersion for Geyser itself.

## 11.2. Install ViaVersion

### Step 1: Download ViaVersion

Open:

https://hangar.papermc.io/ViaVersion/ViaVersion

Download a version compatible with your server software.

### Step 2: Stop your server

Stop the server through the BaoHost panel.

### Step 3: Open the plugins folder

Navigate to:

```text
plugins/
```

### Step 4: Upload ViaVersion

Upload the ViaVersion `.jar` file into the plugins directory.

Your files may look like this:

```text
plugins/
├── Geyser-Spigot.jar
├── floodgate-spigot.jar
└── ViaVersion.jar
```

The actual filenames may vary.

### Step 5: Start the server

Start the server and wait for it to load.

### Step 6: Check for errors

Verify that ViaVersion loaded correctly.

If you see compatibility errors, check the official ViaVersion documentation and your Minecraft server version.

Official documentation:

https://docs.viaversion.com/

## 11.3. Install ViaBackwards

Skip this section if you do not need older Java clients to connect.

### Step 1: Confirm ViaVersion is installed

ViaBackwards requires ViaVersion.

Do not install ViaBackwards alone.

### Step 2: Download ViaBackwards

Official source:

https://hangar.papermc.io/ViaVersion/ViaBackwards

### Step 3: Stop the server

Stop the server through BaoHost.

### Step 4: Upload ViaBackwards

Upload the ViaBackwards `.jar` file into the same plugins directory.

Example:

```text
plugins/
├── Geyser-Spigot.jar
├── floodgate-spigot.jar
├── ViaVersion.jar
└── ViaBackwards.jar
```

### Step 5: Start the server

Start the server and check the console for errors.

### Step 6: Test old Java clients

Join using an older Java client that is supported by your installed ViaVersion and ViaBackwards releases.

Not every older version is supported by ViaBackwards. Read the compatibility information before promising players that a specific old client can join.

Official source:

https://github.com/ViaVersion/ViaBackwards

---

# 12. Configure GeyserMC

This is one of the most important steps.

Geyser must know where to accept Bedrock connections and how to connect to the Java server.

## Step 1: Open Geyser's configuration file

For the Spigot/Paper plugin, the common path is:

```text
plugins/Geyser-Spigot/config.yml
```

Some server implementations or plugin versions may use a different path.

Open the file using the BaoHost file editor.

## Step 2: Find the `bedrock` section

You will see a section that controls the Bedrock listener.

A simplified example is:

```yaml
bedrock:
  address: 0.0.0.0
  port: 19132
  transport: nethernet
```

This is an example, not a complete configuration file.

Keep the settings generated by your installed Geyser version and change only what is necessary.

### What does `address` mean?

The address tells Geyser which network interface to listen on.

### What does `port` mean?

The port tells Geyser where Bedrock players should connect.

The number `19132` is a common example. It is not guaranteed to be available on your BaoHost server.

### What does `transport` mean?

The transport determines how Geyser handles Bedrock connections.

Current Geyser versions document NetherNet and compatibility options involving RakNet. Follow the current instructions for the Geyser version and the Bedrock versions you plan to support.

Official configuration guide:

https://geysermc.org/wiki/geyser/setup/

## Step 3: Find the `remote` section

For a common Paper/Spigot setup, the relevant options may look like this:

```yaml
remote:
  address: auto
  port: 25565
  auth-type: floodgate
```

Your actual file may contain additional settings.

### What does `address: auto` mean?

In supported configurations, Geyser can automatically determine the Java server address.

### What does `port: 25565` mean?

This is an example Java server port.

Use the actual port assigned to your BaoHost Java server.

### What does `auth-type: floodgate` mean?

It tells Geyser to use Floodgate authentication.

If your installed Geyser version contains this setting, set it to:

```yaml
auth-type: floodgate
```

Do not create a second `remote` section. Edit the existing one.

## Step 4: Save your file

Save the configuration.

Check the indentation carefully. YAML files rely on spacing, and incorrect indentation can cause configuration errors.

## Step 5: Restart the server

Restart the server through BaoHost after saving the configuration.

Check the console for errors related to Geyser, Floodgate, and ports.

---

# 13. Configure Floodgate

Floodgate lets Bedrock players authenticate without a separate Java Edition account.

## Step 1: Confirm Floodgate is installed

Make sure the Floodgate `.jar` file is in the `plugins` directory.

## Step 2: Confirm that Floodgate loaded

Start the server and inspect the console.

If Floodgate did not load successfully, correct that issue before testing Bedrock authentication.

## Step 3: Configure Geyser to use Floodgate

Open:

```text
plugins/Geyser-Spigot/config.yml
```

Find the authentication setting in the appropriate section.

Use:

```yaml
auth-type: floodgate
```

This setting belongs in Geyser's configuration.

## Step 4: Keep Floodgate files in place

Do not delete Floodgate's generated configuration files or authentication key.

Do not publish the key to GitHub.

## Step 5: Check the whitelist

If your server has a whitelist enabled, Bedrock players may need to be added using their correctly recognized Floodgate usernames.

Check the official Floodgate and Geyser documentation:

https://geysermc.org/wiki/floodgate/setup/

https://geysermc.org/wiki/geyser/faq/

Do not permanently disable your whitelist just to make crossplay work.

---

# 14. Configure BaoHost Network Ports

This step deserves extra attention because plugin installation alone does not guarantee that Bedrock players can connect.

## 14.1. Understand the Java port

Java servers commonly use TCP port `25565`.

However, BaoHost can assign a different Java port.

Use the address and port shown in your actual panel.

## 14.2. Understand the Bedrock port

Geyser traditionally uses port `19132` as its default.

The actual port depends on your configuration and hosting provider.

Current Geyser versions can use transports that require both TCP and UDP on the Bedrock listener port.

This is important because the hosting provider must allow the required network traffic.

## 14.3. Open the BaoHost Network or Allocations section

In your BaoHost panel, locate the area that displays server addresses, ports, or network allocations.

Check:

- The Java server's assigned address.
- The Java server's port.
- Whether a separate Geyser port is available.
- Whether the required Bedrock transport is supported.
- Whether the port can be used by Geyser without conflicting with another service.

The wording of the panel may differ.

If you cannot find the required network options, contact BaoHost support before changing configuration values.

## 14.4. Important: BaoHost's shared-port instructions versus current Geyser

BaoHost's published crossplay guide currently instructs users to set:

```yaml
clone-remote-port: true
```

It explains that Geyser then uses the same port as the Java server.

BaoHost's instructions are available here:

https://help.baohost.com/articles/geyser-floodgate-crossplay

However, the current official Geyser setup documentation describes a newer transport that uses TCP and UDP on the Geyser listener port. It also says that the Geyser port cannot be the same as the Paper/Spigot server port.

Official source:

https://geysermc.org/wiki/geyser/setup/

These instructions can conflict when applying a shared-port configuration to a current Geyser version.

**Do not blindly enable `clone-remote-port: true` on a current NetherNet configuration.**

For current Geyser setups, use a separately allocated Bedrock port unless BaoHost confirms that its specific shared-port configuration supports your selected Geyser transport.

If the `clone-remote-port` option exists in your configuration, its proper value depends on the actual port arrangement. Do not add an option that is not present in your version's configuration file.

## 14.5. Recommended method for current Geyser: separate port

Unless BaoHost confirms its shared-port setup supports your configuration, the safer approach is to use a separate Bedrock listener port.

### Step 1: Ask for or locate a Geyser allocation

Use the BaoHost panel to check available allocations.

If you cannot find one, contact BaoHost support and ask for a port suitable for the current Geyser transport.

### Step 2: Record the allocated port

Write down the Bedrock port assigned by BaoHost.

Do not assume `19132` is available.

### Step 3: Configure Geyser's Bedrock port

In Geyser's configuration, set the `bedrock.port` to the assigned value.

For example, if the provider allocates port `19132`, the relevant section might be:

```yaml
bedrock:
  address: 0.0.0.0
  port: 19132
  transport: nethernet
```

Use the actual supported transport setting for your Geyser version.

### Step 4: Confirm the listener does not conflict

The Geyser listener must not conflict with the Java server's listener.

Do not give both services the same TCP listening port on the same network interface.

### Step 5: Check TCP and UDP support

Ask BaoHost whether the allocated port supports the transport required by your current Geyser version.

The current Geyser setup guide documents the port requirements and transport options.

### Step 6: Restart and test

Restart the server and verify that Geyser starts listening successfully.

Then test from a Bedrock client outside the server's local environment.

## 14.6. Optional: compatibility for older Bedrock versions

The current Geyser setup documentation describes NetherNet and a compatibility option involving both NetherNet and RakNet.

If you want compatibility features for Bedrock versions that rely on RakNet for server information, check whether you need the documented `transport: both` configuration and an additional UDP port.

This can require additional network allocations.

Do not add the `webrtc-port` option unless your selected transport and Geyser version require it.

Follow the current instructions here:

https://geysermc.org/wiki/geyser/setup/

## 14.7. What address do Bedrock players use?

Bedrock players need:

- The server address or hostname.
- The Bedrock listener port.

If your hosting provider confirms that a shared-port setup works with your Geyser configuration, players may use the same port number as Java players.

Otherwise, they must use the separate Geyser port.

Always give them the address and port confirmed by your working configuration.

---

# 15. Start the Server and Check the Console

Once the plugins and configuration files are ready, start the server again.

## Step 1: Start the server

Open BaoHost's Console or server management page.

Select Start.

Wait for the server to finish loading.

## Step 2: Check plugin loading

Look for successful startup messages from:

- GeyserMC.
- Floodgate.
- ViaVersion, if installed.
- ViaBackwards, if installed.

The exact wording of these messages can differ between releases.

## Step 3: Check for port errors

Look for messages about:

- Address already in use.
- Failed to bind.
- Unsupported transport.
- Missing or invalid configuration.
- Authentication errors.
- Incompatible Minecraft versions.

If an error appears, correct it before inviting players.

## Step 4: Confirm that Geyser is listening

Check Geyser's startup messages for confirmation that its Bedrock listener started.

If the listener cannot start, verify the assigned port and required transport.

## Step 5: Keep the server running

Do not close or stop the server after testing. It must be running for players to connect.

---

# 16. How Java Players Join

Java players use the normal Java Edition multiplayer connection.

## Instructions for Java players

1. Open Minecraft Java Edition.
2. Select **Multiplayer**.
3. Select **Add Server**.
4. Enter a server name.
5. Enter the BaoHost server address.
6. Enter the Java port when required.
7. Save the server.
8. Join.

Use the Java server address and Java port.

Do not tell Java players to use a separate Bedrock port unless your confirmed network configuration specifically requires it.

If ViaVersion or ViaBackwards is installed, the server may accept additional supported Java client versions.

Compatibility is not unlimited, so test the specific versions you intend to allow.

---

# 17. How Bedrock Players Join

Bedrock players connect through Geyser.

The exact steps depend on their platform.

## 17.1. Android and iOS

1. Open Minecraft Bedrock Edition.
2. Select **Play**.
3. Open the **Servers** tab.
4. Select **Add Server**.
5. Enter a server name.
6. Enter the BaoHost server address or hostname.
7. Enter the Geyser Bedrock port.
8. Save the server.
9. Select the server and join.

Use the Bedrock port specified by the working BaoHost configuration.

## 17.2. Windows Bedrock Edition

Make sure you open Minecraft Bedrock Edition rather than Java Edition.

Then:

1. Select **Play**.
2. Open the **Servers** tab.
3. Select **Add Server**, if available.
4. Enter the server name.
5. Enter the server address.
6. Enter the Bedrock port.
7. Save the server.
8. Join.

## 17.3. What if Bedrock says "Unable to Connect to World"?

Check:

- The IP address or hostname.
- The port.
- The server's online status.
- Geyser's startup messages.
- BaoHost's network allocation.
- Whether the Bedrock client version is supported.

If the address and port are correct but the connection still fails, review the troubleshooting section.

---

# 18. Console Players: Xbox, PlayStation and Nintendo Switch

Console support requires an extra explanation.

Xbox, PlayStation, and Nintendo Switch do not all provide the same direct custom-server connection options available on mobile and Windows Bedrock.

Some console players may need an alternative method to connect to a custom server.

Official Geyser console documentation:

https://geysermc.org/wiki/geyser/using-geyser-with-consoles/

Check the instructions for the specific console and game version.

Do not promise that all console players can enter an arbitrary server IP directly through their normal Servers menu.

The server-side setup can be correct even when a console player still needs a platform-specific connection method.

---

# 19. Testing That Crossplay Works

Once both editions can connect, perform a full test.

## Test 1: Java connection

Join the server from Java Edition.

Confirm that the player can enter the world.

## Test 2: Bedrock connection

Join the same server from Bedrock Edition using Geyser's address and port.

Confirm that the player can enter the world.

## Test 3: Check that both players see each other

Have the Java and Bedrock players stand near each other.

Confirm that each player can see the other player in the world.

## Test 4: Test normal gameplay

Check:

- Movement.
- Chat.
- Block breaking.
- Block placement.
- Inventory access.
- Basic survival gameplay.

Different editions can have different mechanics, so some behavior may not be identical.

## Test 5: Check authentication

If you installed Floodgate, confirm that Bedrock players can authenticate without being asked to use a separate Java Edition account.

## Test 6: Test version compatibility

If ViaVersion and ViaBackwards are installed, test the Java versions you want to support.

Do not assume all versions work simply because one test succeeds.

## Test 7: Check after restarting

Restart the server once more and repeat the most important connection tests.

This confirms that the setup works after a normal restart rather than only immediately after configuration.

---

# 20. Troubleshooting

## Problem 1: Bedrock players cannot join

### Possible causes

- Incorrect IP address.
- Incorrect Geyser port.
- Missing network allocation.
- The required TCP or UDP transport is not available.
- Geyser failed to start.
- Unsupported Bedrock client version.
- Incorrect transport configuration.

### Solutions

1. Verify the address and port.
2. Check Geyser's `bedrock` configuration.
3. Confirm the network allocation with BaoHost.
4. Check the server console for listener errors.
5. Verify the Geyser supported-version list.
6. Ask BaoHost support to check the assigned port if the problem persists.

---

## Problem 2: Java works, but Bedrock does not

A Java connection working does not prove that Geyser's listener is available.

Check the Bedrock listener separately.

Confirm:

- The Geyser port.
- The transport.
- BaoHost's network allocation.
- The relevant console startup messages.
- Whether Geyser is configured to use the correct port arrangement.

If using the latest Geyser transport, verify whether a separate port is required.

---

## Problem 3: Bedrock players are asked for a Java account

### Possible causes

- Floodgate is missing.
- Floodgate failed to load.
- Geyser is not using Floodgate authentication.
- The installed components are incompatible.

### Solutions

1. Verify the Floodgate plugin.
2. Check that it loaded successfully.
3. Open Geyser's configuration.
4. Verify the authentication setting:

```yaml
auth-type: floodgate
```

5. Save the file.
6. Restart the server.
7. Try joining again.

Official Floodgate setup:

https://geysermc.org/wiki/floodgate/setup/

---

## Problem 4: Geyser cannot bind to its port

### Possible causes

- The port is already being used.
- The port allocation is invalid.
- The port is conflicting with the Java server.
- BaoHost does not permit the requested network arrangement.
- The configuration is incompatible with the selected transport.

### Solutions

1. Check the configured Bedrock port.
2. Compare it with your BaoHost allocations.
3. Confirm the required transport with BaoHost support.
4. Avoid assigning the same TCP listening port to Geyser and the Java server on the same interface.
5. Restart after correcting the configuration.

Do not change ports randomly without confirming that they are allocated and supported.

---

## Problem 5: Geyser is not compatible with my server version

### Possible causes

- The Java server is too old.
- The server protocol does not match the protocol required by Geyser.
- The installed Geyser release does not support the server setup.

### Solutions

1. Open the official Geyser supported-version page.
2. Check your Java server version.
3. Check the required Java runtime.
4. Determine whether ViaVersion is required.
5. If your server is below the minimum supported version for direct Geyser-Spigot installation, follow the appropriate proxy or alternative setup.

Official supported versions:

https://geysermc.org/wiki/geyser/supported-versions/

ViaVersion does not make every old server compatible with every new Geyser version.

---

## Problem 6: ViaVersion fails to load

### Possible causes

- Incorrect plugin version.
- Unsupported server software.
- Unsupported Java runtime.
- A compatibility issue with another plugin.

### Solutions

1. Check the ViaVersion download source.
2. Confirm your server software is supported.
3. Verify your Java runtime.
4. Read the console error.
5. Consult the official documentation.

Official setup:

https://viaversion.com/setup

---

## Problem 7: ViaBackwards fails to load

ViaBackwards requires ViaVersion.

Confirm that:

- ViaVersion is installed.
- ViaVersion loads successfully.
- Both plugins support your server version.
- The correct `.jar` files were uploaded.

Do not install ViaBackwards on its own.

---

## Problem 8: Older Java clients still cannot join

ViaVersion and ViaBackwards only support particular version combinations.

Check the supported versions for your installed releases.

Some older versions may require additional compatibility components, or may not be supported at all.

Do not assume ViaBackwards supports every old client.

---

## Problem 9: Floodgate players cannot join a whitelisted server

The server may be rejecting the Bedrock player because the whitelist does not contain the username it recognizes.

Check the Floodgate documentation and the server console.

Add the correct account to the whitelist if appropriate.

Do not permanently disable the whitelist as a workaround.

---

## Problem 10: The server crashes after installing plugins

### Possible causes

- Incompatible plugin builds.
- Incorrect server software.
- A damaged download.
- Incorrect configuration.
- Java runtime incompatibility.
- A conflict with another plugin.

### Solutions

1. Stop the server.
2. Read the full error from the console or crash report.
3. Identify which plugin caused the failure.
4. Verify compatibility against the official project pages.
5. Restore your backup if necessary.
6. Reinstall compatible files.

Do not delete your world or all plugin files as the first troubleshooting step.

---

## Problem 11: Crossplay stops working after an update

Minecraft updates can change protocol requirements.

Geyser, Floodgate, ViaVersion, ViaBackwards, and the server software may need compatible releases.

### Solutions

1. Check the current Geyser supported versions.
2. Read the latest plugin release notes.
3. Verify that the server software is still compatible.
4. Back up your server before updating.
5. Restart and retest both editions.

---

# 21. Frequently Asked Questions

## Q1. Do I need GeyserMC?

Yes, for the plugin-based Java-Bedrock crossplay setup in this guide.

Geyser is the component that bridges Bedrock players to a Java server.

## Q2. Do I need Floodgate?

Floodgate is recommended if Bedrock players should be able to authenticate without a separate Java Edition account.

Without Floodgate, a different authentication arrangement is required.

## Q3. Do I need ViaVersion?

It depends on your Java server version and the protocol required by the current Geyser release.

Check the official supported-version page.

For the current Geyser protocol, ViaVersion may be required when the backend server does not accept the protocol used by Geyser.

## Q4. Do I need ViaBackwards?

No, not just for Bedrock crossplay.

ViaBackwards is for allowing supported older Java clients to connect to a newer Java server. It requires ViaVersion.

## Q5. Can I use an existing world?

Yes, normally. A compatible Java server can usually keep its existing world when Geyser and Floodgate are added.

Make a backup first.

## Q6. Can I use Paper?

Yes. Paper is a good choice for the plugin installation method in this guide.

## Q7. Can I use Purpur?

Yes, when your Purpur version and plugins are compatible.

## Q8. Can I use Vanilla?

Not for the Paper/Spigot plugin method described here. Vanilla does not load those plugins directly.

Use compatible server software or a different Geyser setup.

## Q9. Can Bedrock players join without owning Java Edition?

Yes, when Floodgate and Geyser are configured correctly.

## Q10. Can Xbox, PlayStation, and Switch players join?

Potentially, but console platforms can require additional connection steps. Check the official Geyser console documentation for your specific device.

## Q11. Do Java and Bedrock players use the same port?

Not necessarily.

BaoHost documents a shared-port method using `clone-remote-port: true`. However, current Geyser transport requirements may require a separate Bedrock port.

Follow the current Geyser documentation and confirm what BaoHost supports before using the shared-port method.

## Q12. Can I install all four plugins at once?

You can install compatible plugins together, but there is no need to install ViaBackwards unless older Java client support is required.

Start with the necessary plugins for your server version, then add optional compatibility components when needed.

## Q13. Will every plugin work for Bedrock players?

No. Some Java server plugins depend on features that Bedrock clients do not support identically.

Test the plugins and gameplay features you intend to use.

## Q14. Can I use mods?

It depends on the server software and the mods.

Geyser does not automatically make every client-side Java mod compatible with Bedrock Edition.

Check the official Geyser documentation and the requirements of individual mods.

## Q15. Why can a Bedrock player see the server but not join?

Possible causes include an unsupported protocol, an authentication failure, a port problem, or a configuration issue.

Check the server console and Geyser logs.

---

# 22. Final Setup Checklist

Use this checklist before inviting your friends.

## Server setup

- [ ] BaoHost server is running compatible Java Edition server software.
- [ ] Paper, Purpur, or Spigot is selected for the plugin installation method.
- [ ] Server version is compatible with the current Geyser release.
- [ ] Java runtime satisfies the server and plugin requirements.
- [ ] A backup of the world and configuration has been created.

## GeyserMC and Floodgate

- [ ] GeyserMC was downloaded from the official source.
- [ ] Floodgate was downloaded from the official source.
- [ ] Both `.jar` files are in the correct plugins directory.
- [ ] Both plugins loaded successfully.
- [ ] Geyser is configured to use Floodgate authentication.
- [ ] The Floodgate authentication key is not publicly shared.

## Version compatibility

- [ ] ViaVersion was installed if required by the server version.
- [ ] ViaBackwards was installed only if older Java clients need support.
- [ ] Plugin versions are compatible with the server.
- [ ] Supported client versions have been checked against official documentation.

## Network configuration

- [ ] Java server address and port are correct.
- [ ] Geyser's Bedrock listener port is configured.
- [ ] BaoHost supports the required network transport.
- [ ] The Bedrock port does not conflict with another listener.
- [ ] Shared-port settings are used only if supported by the actual configuration.
- [ ] The address and port given to Bedrock players are correct.

## Testing

- [ ] The server starts without relevant plugin errors.
- [ ] A Java player can connect.
- [ ] A Bedrock player can connect.
- [ ] Both editions can enter the same world.
- [ ] Both players can see each other.
- [ ] Authentication works as expected.
- [ ] The server still works after restarting.

## Security

- [ ] Floodgate keys are not published.
- [ ] Private server credentials are not committed to GitHub.
- [ ] Whitelist and security settings remain configured appropriately.
- [ ] Backups are available before future updates.

---

# 23. Official Documentation and Resources

| Resource | Link |
|---|---|
| BaoHost website | https://baohost.com |
| BaoHost Help Center | https://help.baohost.com/ |
| BaoHost Geyser + Floodgate guide | https://help.baohost.com/articles/geyser-floodgate-crossplay |
| GeyserMC website | https://geysermc.org/ |
| GeyserMC downloads | https://geysermc.org/download |
| GeyserMC setup guide | https://geysermc.org/wiki/geyser/setup/ |
| GeyserMC supported versions | https://geysermc.org/wiki/geyser/supported-versions/ |
| GeyserMC FAQ | https://geysermc.org/wiki/geyser/faq/ |
| GeyserMC console guide | https://geysermc.org/wiki/geyser/using-geyser-with-consoles/ |
| Floodgate setup | https://geysermc.org/wiki/floodgate/setup/ |
| Paper downloads | https://papermc.io/downloads/paper |
| ViaVersion downloads | https://hangar.papermc.io/ViaVersion/ViaVersion |
| ViaVersion documentation | https://docs.viaversion.com/ |
| ViaVersion setup generator | https://viaversion.com/setup |
| ViaBackwards downloads | https://hangar.papermc.io/ViaVersion/ViaBackwards |
| ViaBackwards GitHub | https://github.com/ViaVersion/ViaBackwards |

---

# Conclusion

Setting up crossplay on BaoHost requires a compatible Minecraft Java server, GeyserMC, a suitable network configuration, and optionally Floodgate and version compatibility plugins.

The recommended starting point is:

1. Select compatible Paper server software.
2. Install GeyserMC.
3. Install Floodgate.
4. Configure Geyser authentication.
5. Set up the Bedrock network listener using a port arrangement supported by BaoHost and your Geyser version.
6. Install ViaVersion if the current Geyser protocol requires it for your backend server.
7. Install ViaBackwards only if you want supported older Java clients to join.
8. Start the server and test with both Minecraft editions.

The most important thing is to make sure that the server version, plugin versions, authentication settings, and network ports all match the requirements of your specific installation.

**Do not blindly copy example port numbers or old configuration snippets.** Verify the current official documentation and the settings displayed in your BaoHost panel before making changes.

Once the plugins load successfully and both Java and Bedrock players can connect, your server is ready for crossplay testing.
