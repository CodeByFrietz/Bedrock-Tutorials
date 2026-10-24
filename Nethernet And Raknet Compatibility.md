# Minecraft Java and Bedrock: NetherNet vs. RakNet Compatibility Guide

A beginner-friendly guide explaining how Minecraft Java Edition and Bedrock Edition connect to multiplayer servers, what NetherNet and RakNet mean, how they differ, and which connection method a server owner should use.

**Last reviewed:** October 24, 2026

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Understanding Java Edition and Bedrock Edition](#2-understanding-java-edition-and-bedrock-edition)
3. [What Is a Network Transport?](#3-what-is-a-network-transport)
4. [What Is RakNet?](#4-what-is-raknet)
5. [What Is NetherNet?](#5-what-is-nethernet)
6. [NetherNet vs. RakNet](#6-nethernet-vs-raknet)
7. [How Java and Bedrock Players Connect](#7-how-java-and-bedrock-players-connect)
8. [Which Transport Should You Choose?](#8-which-transport-should-you-choose)
9. [Understanding the Transport Settings](#9-understanding-the-transport-settings)
10. [Network Ports Explained](#10-network-ports-explained)
11. [Using NetherNet on BaoHost](#11-using-nethernet-on-baohost)
12. [Using Both NetherNet and RakNet](#12-using-both-nethernet-and-raknet)
13. [Bedrock Compatibility and Version Changes](#13-bedrock-compatibility-and-version-changes)
14. [How Java Players Are Affected](#14-how-java-players-are-affected)
15. [Common Problems and Solutions](#15-common-problems-and-solutions)
16. [Frequently Asked Questions](#16-frequently-asked-questions)
17. [Final Checklist](#17-final-checklist)
18. [Official Resources](#18-official-resources)

---

# 1. Introduction

Minecraft Java Edition and Minecraft Bedrock Edition are two different editions of Minecraft.

Java Edition is primarily used on computers, while Bedrock Edition is used on mobile devices, Windows, Xbox, PlayStation, and Nintendo Switch.

Although both editions allow players to explore the same general Minecraft experience, they use different networking systems. This means that a normal Java Edition server does not automatically allow Bedrock Edition players to join.

When a Java server is configured to accept Bedrock players, a compatible bridging program or plugin is needed to translate the communication between the two editions.

For example, GeyserMC is a commonly used bridge that allows Bedrock players to join a Java server.

However, the bridge still needs to know how Bedrock players will connect.

This is where **RakNet** and **NetherNet** become important.

They are two different ways that Bedrock clients can establish their network connection.

This guide explains their differences in simple terms and clarifies which settings affect Java players and which affect Bedrock players.

## The most important thing to understand

- Java players continue connecting to the Java server normally.
- Bedrock players connect through a compatible bridge when joining a Java server.
- RakNet and NetherNet describe the Bedrock connection method.
- Changing the Bedrock transport does not mean Java players must switch to NetherNet or RakNet.

**If you are running a Java server with Bedrock crossplay, the transport setting mainly concerns how Bedrock players reach the server.**

---

# 2. Understanding Java Edition and Bedrock Edition

Before comparing the transports, it helps to understand how the two editions connect to multiplayer servers.

## 2.1. Minecraft Java Edition

Java Edition is primarily used on:

- Windows
- macOS
- Linux

Java players connect to a Minecraft Java server using the Java Edition network protocol.

A Java server commonly uses TCP port `25565`, although a hosting provider can assign a different port.

For example:

```text
Java server address: play.example.com
Java server port:    25565
```

The address and port above are examples, not a real server.

When a Java player joins, the client connects to the Java server using the protocol expected by that server.

**Java players do not select RakNet or NetherNet in the normal Minecraft multiplayer menu.**

Those are Bedrock transport options, not Java Edition connection settings.

## 2.2. Minecraft Bedrock Edition

Bedrock Edition is available on platforms such as:

- Android
- iOS
- Windows Bedrock Edition
- Xbox
- PlayStation
- Nintendo Switch

Bedrock uses a different networking protocol from Java Edition.

A normal Java server therefore cannot directly understand a Bedrock connection.

When Bedrock players want to join a Java server, a compatible bridge must translate their communication.

The bridge also needs to accept the Bedrock connection using a transport supported by the client.

RakNet and NetherNet are relevant at this stage.

## 2.3. Does a Java server need Bedrock crossplay?

No.

A Java server can run normally without accepting Bedrock players.

If you only want Java players to join, you do not need to choose a Bedrock transport.

RakNet and NetherNet matter when your server is configured to accept Bedrock connections.

## 2.4. What if I want both Java and Bedrock players?

The setup generally looks like this:

```text
                  MINECRAFT SERVER
                         |
                  Java Edition Server
                         |
             +-----------+-----------+
             |                       |
             |                       |
       Java Players             Bedrock Bridge
             |                       |
     Normal Java Protocol      Bedrock Transport
                                     |
                           +---------+---------+
                           |                   |
                        NetherNet            RakNet
                           |                   |
                      Bedrock Player      Compatible Older
                                             Bedrock Player
```

The exact connection arrangement depends on the software and configuration being used.

The important distinction is that Java players use the normal Java connection, while Bedrock players use the Bedrock connection accepted by the bridge.

---

# 3. What Is a Network Transport?

A network transport describes how two programs exchange data over a network.

For Minecraft, the transport affects how the game client establishes and maintains its connection to a server.

RakNet and NetherNet are different connection systems associated with Minecraft Bedrock Edition.

The choice of transport can affect:

- Which Bedrock clients can connect.
- How the server discovers and establishes a connection.
- Which network ports must be available.
- Whether TCP is required in addition to UDP.
- Whether an older Bedrock client can display the server's description and player count correctly.

## Simple example

Imagine a Minecraft server as a building.

The server is the destination, but different players may need different entrances.

Java players use the Java connection.

Bedrock players use a Bedrock-compatible connection.

RakNet and NetherNet are different ways for Bedrock players to establish that connection.

The destination world remains the same. The connection method is what changes.

---

# 4. What Is RakNet?

RakNet is the traditional networking method used by Minecraft Bedrock Edition.

In a traditional RakNet connection, a Bedrock player communicates directly with the server over UDP.

UDP is a network protocol that allows data to be exchanged between devices without establishing a TCP connection first.

In a Java crossplay setup, the Bedrock connection is received by the compatible bridge, which then communicates with the Java server.

A simplified example looks like this:

```text
Bedrock Player
      |
      | RakNet over UDP
      |
      v
Bedrock-Compatible Bridge
      |
      | Java Protocol
      |
      v
Minecraft Java Server
```

## 4.1. How RakNet works

The connection process is approximately:

1. The Bedrock player selects the server.
2. The Bedrock client attempts to connect using RakNet.
3. The server's Bedrock listener receives the connection.
4. The bridge processes the Bedrock communication.
5. The player joins the Minecraft world.

## 4.2. Advantages of RakNet

RakNet is useful for understanding older Bedrock connections and maintaining compatibility with supported legacy clients.

Its advantages include:

- It is the traditional Bedrock transport.
- Existing guides may already describe it.
- Older supported clients may rely on RakNet for server-list information.
- Some clients may need it to retrieve the server's MOTD and player count.

**MOTD** means "Message of the Day." It is the description shown in a server list.

RakNet's role in connecting players should not be confused with its role in retrieving server-list information.

A client might use one method to retrieve information about a server and another method to establish its gameplay connection.

## 4.3. Limitations of RakNet

RakNet is not the long-term connection method for every future Bedrock release.

Minecraft Bedrock is transitioning to NetherNet.

As clients move to the new transport, servers that only support RakNet may stop accepting those clients.

Therefore, a new server should not rely on RakNet-only mode without checking the current compatibility requirements.

Official migration announcement:

https://geysermc.org/blog/preparing-for-nethernet/

---

# 5. What Is NetherNet?

NetherNet is the newer networking transport being introduced for Minecraft Bedrock Edition.

Unlike the traditional direct RakNet connection, NetherNet uses a signaling stage before establishing its gameplay connection.

In the current Geyser implementation, signaling uses TCP, while gameplay communication uses WebRTC over UDP.

These are technical details of the networking process, but the practical difference is straightforward:

**NetherNet needs an additional step to establish the connection before the Bedrock player can enter the game.**

## 5.1. How NetherNet works

A simplified connection looks like this:

```text
              Bedrock Player
                    |
                    |
             1. Signaling Request
                  over TCP
                    |
                    v
             Signaling Service
                    |
                    |
          2. Returns Connection Details
                    |
                    v
           WebRTC Gameplay Connection
                  over UDP
                    |
                    v
        Bedrock-Compatible Bridge
                    |
                    |
              Java Protocol
                    |
                    v
          Minecraft Java Server
```

The signaling stage helps the client obtain the information necessary to connect.

The gameplay connection then uses WebRTC over UDP.

## 5.2. What does signaling mean?

Signaling is the process used to exchange the information needed to establish a connection.

Think of it as an introduction before two devices begin communicating directly.

The client first asks how to connect. The signaling service provides the necessary connection information, and the client then establishes the gameplay connection.

Signaling is not the Minecraft world itself. It is part of the process of establishing the connection.

## 5.3. Advantages of NetherNet

NetherNet is important because Bedrock is moving toward this newer transport.

Its advantages include:

- Compatibility with newer Bedrock connection behavior.
- Support for signaling-based connection establishment.
- Support for newer Bedrock clients that use NetherNet.
- Server-list information can be retrieved through signaling.

## 5.4. What changes for a server owner?

The network configuration becomes more important.

With RakNet, a traditional setup could rely on UDP.

With NetherNet, the built-in signaling method also needs a reachable TCP port.

The gameplay connection still requires UDP.

Therefore, a server may be configured correctly for UDP but still fail to appear or connect if the necessary TCP signaling port is unavailable.

Official explanation:

https://geysermc.org/blog/preparing-for-nethernet/

---

# 6. NetherNet vs. RakNet

The following table compares the two transports.

| Feature | RakNet | NetherNet |
|---|---|---|
| Main purpose | Traditional Bedrock connection | Newer Bedrock connection |
| Connection process | Direct connection over UDP | Signaling followed by WebRTC |
| Initial signaling | Does not use the new NetherNet signaling process | Uses signaling over TCP in the built-in Geyser setup |
| Gameplay connection | UDP | WebRTC over UDP |
| Port requirements | Traditionally UDP | TCP and UDP for the main built-in signaling setup |
| Older Bedrock compatibility | Useful for supported legacy clients | Depends on client version and support |
| Newer Bedrock compatibility | Being phased out | The recommended transport for newer Bedrock clients |
| Java Edition player settings | Not applicable | Not applicable |
| Bedrock server-list compatibility | Used by some older clients | Newer clients use signaling for server information |
| Geyser transport value | `raknet` | `nethernet` |
| Combined compatibility | Can be enabled alongside NetherNet | Can be enabled alongside RakNet using `both` |

The table describes the transport behavior in a Geyser-based Java server setup. Exact compatibility depends on the installed bridge version and Minecraft client version.

## The main difference in one sentence

**RakNet is the traditional Bedrock connection method, while NetherNet introduces signaling over TCP before establishing gameplay communication over UDP.**

## Why does this matter?

It affects how the server must be configured.

For example:

- A RakNet-only configuration may not accept a Bedrock client that requires NetherNet.
- A NetherNet configuration needs the necessary signaling and gameplay networking.
- A combined configuration needs a separate UDP port for NetherNet when RakNet is also enabled.

Java Edition players continue using the normal Java connection in all these cases.

---

# 7. How Java and Bedrock Players Connect

This section explains what actually happens when both editions use the same Java-hosted world.

## 7.1. Java player connection

A Java player:

1. Opens Minecraft Java Edition.
2. Selects Multiplayer.
3. Enters the Java server address.
4. Connects using the Java Edition protocol.
5. Joins the world.

The player does not need to know whether the Bedrock side uses RakNet or NetherNet.

## 7.2. Bedrock player connection

A Bedrock player:

1. Opens Minecraft Bedrock Edition.
2. Selects the server or enters the required address.
3. Establishes the connection using a supported Bedrock transport.
4. Reaches the compatible bridge.
5. Joins the Java server through that bridge.

The transport setting determines how the Bedrock connection is accepted.

## 7.3. Do Java players need to change their client settings?

No.

Java players do not select NetherNet or RakNet.

Their Minecraft client continues connecting normally to the Java server.

The Java server owner may need to configure the crossplay bridge and its network ports, but that does not mean Java players must change how they join.

## 7.4. Does NetherNet convert Java into Bedrock?

No.

NetherNet does not convert Java Edition into Bedrock Edition.

It is a Bedrock transport.

The bridge is responsible for translating the Bedrock connection into communication that the Java server can process.

## 7.5. Can Java and Bedrock players be in the same world?

Yes, when the Java server and its crossplay bridge are configured correctly.

The two groups connect through different network paths, but their sessions can reach the same Java-hosted world.

Some gameplay features can still behave differently because Java and Bedrock are not identical editions.

---

# 8. Which Transport Should You Choose?

The best setting depends on which Bedrock clients you need to support.

## Option A: NetherNet

Use NetherNet when your goal is to support newer Bedrock clients and your server has the required network configuration.

Example:

```yaml
bedrock:
  port: 19132
  transport: nethernet
```

This is a simplified configuration example.

The port must be available for the required TCP and UDP traffic in a built-in signaling setup. Your hosting provider may require a different port.

For a new crossplay server, NetherNet is the recommended direction.

## Option B: RakNet

RakNet-only mode may be appropriate for a legacy configuration with supported older clients.

However, it should not be treated as the long-term answer for newer Bedrock versions.

Example:

```yaml
bedrock:
  port: 19132
  transport: raknet
```

This is an illustrative example, not a recommendation to use RakNet-only mode for a new server.

Check the compatibility requirements before choosing this setting.

## Option C: Both NetherNet and RakNet

Choose both when you need NetherNet while retaining compatibility with certain supported older Bedrock clients or their server-list behavior.

Example:

```yaml
bedrock:
  port: 19132
  webrtc-port: 19133
  transport: both
```

These port numbers are examples. Do not copy them unless the hosting provider has allocated the required ports.

In this setup:

- The main listener is configured on the specified `port`.
- NetherNet uses the separate `webrtc-port` for gameplay over UDP.
- The main port must also support the required signaling and RakNet traffic.
- The two transports cannot use the same UDP port in combined mode.

## Which is best for a new server?

For a new server, start by checking whether NetherNet alone supports the Bedrock clients you want to accept.

Use both transports only when you have a specific compatibility requirement.

Do not select RakNet-only mode for a new server without confirming current Bedrock support.

---

# 9. Understanding the Transport Settings

The following examples use a typical Geyser configuration file:

```text
plugins/Geyser-Spigot/config.yml
```

The actual path can vary depending on the server software.

These examples are only the relevant settings, not complete replacement configuration files.

## 9.1. NetherNet configuration

```yaml
bedrock:
  port: 19132
  transport: nethernet
```

This tells the bridge to use NetherNet for Bedrock connections.

In the built-in signaling setup, the configured port must support TCP signaling and UDP gameplay.

It must not conflict with another program's listener.

## 9.2. RakNet configuration

```yaml
bedrock:
  port: 19132
  transport: raknet
```

This selects the traditional RakNet transport.

Use it only when it supports the clients and version combinations you intend to allow.

## 9.3. Combined configuration

```yaml
bedrock:
  port: 19132
  webrtc-port: 19133
  transport: both
```

This enables both transport methods.

`webrtc-port` specifies a separate UDP port for NetherNet gameplay.

The port numbers above are examples. The additional port must be available and configured correctly with the hosting provider.

## 9.4. Important configuration rules

- Keep the existing configuration file and edit only the necessary settings.
- Do not create duplicate `bedrock` sections.
- Check the YAML indentation.
- Confirm all required ports are allocated.
- Restart the server after making changes.
- Read the server console for errors.
- Follow the documentation for the exact installed version of the bridging software.

Official setup instructions:

https://geysermc.org/wiki/geyser/setup/

---

# 10. Network Ports Explained

This is important for anyone hosting the server.

A port identifies a network endpoint used by an application.

The number alone does not describe the entire connection. TCP and UDP are different network protocols, even when the numeric port is the same.

## 10.1. Java server port

Java Edition commonly uses TCP port `25565`.

Your hosting provider may assign a different port.

Java players connect using the Java address and port.

## 10.2. NetherNet main port

In the built-in signaling setup, NetherNet uses a main port for signaling over TCP and gameplay-related networking over UDP.

For example:

```text
Port: 19132
TCP:  Required for signaling
UDP:  Required for gameplay
```

This is an example, not a guaranteed BaoHost allocation.

## 10.3. Additional port for both transports

When `transport: both` is selected, NetherNet needs a separate UDP port.

For example:

```text
Main port:       19132
NetherNet port:  19133
```

The second port must be available for UDP.

## 10.4. Why cannot NetherNet always share the Java port?

The Java server normally listens on TCP.

The built-in NetherNet signaling service also needs a TCP listener.

Two different services cannot ordinarily bind to the same TCP address and port simultaneously.

As a result, a traditional crossplay setup that shared the Java port may need a different arrangement for NetherNet.

## 10.5. Can the same number be used for TCP and UDP?

Yes, provided the hosting environment permits both protocols and there are no conflicting listeners.

TCP port `19132` and UDP port `19132` are separate endpoints.

However, the fact that TCP and UDP are separate does not mean that two TCP services can use the same TCP address and port.

## 10.6. What if BaoHost only provides one port?

Do not assume that the existing shared-port configuration will automatically work with every NetherNet setup.

There are different approaches, including:

- Asking BaoHost for a separate port that supports the required networking.
- Using a supported external signaling configuration.
- Following a hosting-provider-specific setup.

The appropriate method depends on how the host manages networking.

See the BaoHost section below.

---

# 11. Using NetherNet on BaoHost

BaoHost has its own server panel and port-allocation arrangement.

Its crossplay guide has historically recommended sharing the Java and Bedrock port with `clone-remote-port: true`.

However, the current NetherNet requirements change how this arrangement works.

The built-in NetherNet signaling listener cannot ordinarily use the same TCP address and port as the Java server.

The official Geyser documentation explains that `clone-remote-port` works with external signaling in this situation.

## Step 1: Open your BaoHost panel

Log in to BaoHost and select your Minecraft Java server.

## Step 2: Check the available ports

Look for the Network, Allocations, or Ports section.

Write down:

- The Java server address.
- The Java server port.
- Any separate port allocated for Bedrock crossplay.
- Whether the required TCP and UDP traffic is supported.

## Step 3: Choose a supported arrangement

### If you have a separate Geyser port

Use the port allocated for the crossplay service.

Make sure it supports TCP and UDP for the built-in NetherNet signaling setup.

Configure the bridge to use that port.

### If you only have the Java server port

Do not assume that a basic shared-port configuration will support built-in NetherNet signaling.

Consult the latest Geyser instructions for hosting providers without a separate port.

Depending on the setup, the bridge may use external signaling. In that case, the connection address provided to Bedrock players may differ from the regular Java address.

Read the console output and provide players with the address shown by the working setup.

## Step 4: Do not blindly copy old port instructions

A previous crossplay guide may have said to set:

```yaml
clone-remote-port: true
```

That option shares the Java server's port in supported configurations.

However, it does not remove the TCP port conflict associated with built-in NetherNet signaling.

Follow the current documentation and confirm which signaling arrangement is in use.

## Step 5: Restart and test

After editing the settings:

1. Save the configuration.
2. Restart the server.
3. Check the console.
4. Confirm that signaling starts correctly.
5. Test a Bedrock connection.
6. Verify that Java players can still join normally.

## BaoHost resources

BaoHost crossplay tutorial:

https://help.baohost.com/articles/geyser-floodgate-crossplay

Official NetherNet migration guide:

https://geysermc.org/blog/preparing-for-nethernet/

Official setup instructions:

https://geysermc.org/wiki/geyser/setup/

If the panel does not make it clear which ports support the required protocols, contact BaoHost support before changing the configuration.

---

# 12. Using Both NetherNet and RakNet

Combined mode is useful when some supported Bedrock clients need RakNet while newer clients use NetherNet.

One important reason for this option is server-list compatibility.

Some versions, including Bedrock 26.40, fetch the MOTD and player count using RakNet.

This means combined mode may be useful even if a player can establish gameplay through NetherNet.

## Example

```yaml
bedrock:
  port: 19132
  webrtc-port: 19133
  transport: both
```

These port numbers are examples only.

## What must be configured?

1. The main port must be available for the required signaling and RakNet traffic.
2. The `webrtc-port` must be an available, separate UDP port.
3. The hosting network must permit the necessary TCP and UDP traffic.
4. The configuration must match the installed version of the bridge.
5. The server must be restarted after making changes.

## Why must the two UDP ports be different?

The two transports cannot use the same UDP port in combined mode.

The separate `webrtc-port` allows NetherNet gameplay to use its own UDP endpoint.

## Do Java players need the additional port?

No.

The additional port relates to NetherNet and Bedrock transport compatibility.

Java players continue connecting to the Java server normally.

---

# 13. Bedrock Compatibility and Version Changes

Bedrock connection behavior changes over time.

As newer clients adopt NetherNet, server owners must make sure their crossplay setup supports the transport those clients use.

## Status as of October 24, 2026

The official Geyser migration article published on October 8, 2026, announced that Minecraft Bedrock 26.60 was planned for October 27, 2026.

The article stated that clients in that release would stop connecting over RakNet.

As October 24 is before that planned release date, check the live release notes and Geyser compatibility information before publishing or applying this guidance later.

Official announcement:

https://geysermc.org/blog/preparing-for-nethernet/

## What does the transition mean for a server owner?

A RakNet-only setup may no longer be sufficient for newer Bedrock clients after they stop using that transport.

Preparing NetherNet support helps avoid connection problems when players update.

## What about older Bedrock clients?

Some older client versions may still use RakNet for certain operations, such as retrieving the server's MOTD and player count.

Combined mode can preserve this compatibility when the installed bridge supports those clients.

However, older client support is not guaranteed indefinitely. Check which versions are supported by your installed release.

## Should I install both transports permanently?

Not necessarily.

Use the combination only when there is a specific compatibility reason.

Once all the Bedrock clients you support use NetherNet and no longer need RakNet for the relevant behavior, a NetherNet-only configuration may be simpler.

Verify the actual client versions and release status before removing RakNet.

---

# 14. How Java Players Are Affected

This section is important because Java players do not use the same transport settings as Bedrock players.

## Java players continue connecting normally

A Java player:

1. Opens Minecraft Java Edition.
2. Opens Multiplayer.
3. Enters the server address and Java port.
4. Connects to the Java server.

The Java player does not choose NetherNet or RakNet.

## Does enabling NetherNet change the Java connection?

Not directly.

NetherNet changes the way supported Bedrock clients establish their connection.

The server owner still needs to make sure the Java server and the crossplay bridge are configured correctly.

## Can Java players join while NetherNet is enabled?

Yes.

Java players continue using the Java server's ordinary connection.

If the crossplay setup is working correctly, Java and Bedrock players can enter the same world through their respective connection paths.

## Does NetherNet require Java players to update?

Not simply because the Bedrock transport changed.

Java protocol compatibility is a separate issue.

If the Java server version changes, or the bridge requires a different Java protocol version, additional compatibility requirements may apply. Check the server's own version requirements separately.

---

# 15. Common Problems and Solutions

## Problem 1: Bedrock players cannot connect after a transport change

Possible causes:

- The selected transport is not supported by the player's client.
- The main port is not reachable over TCP.
- UDP gameplay traffic is blocked.
- A required additional port is missing.
- The configuration contains an error.

Solutions:

1. Check the current Bedrock support information.
2. Verify the transport setting.
3. Check the main port and any additional UDP port.
4. Read the console errors.
5. Verify the required network allocation with BaoHost.

## Problem 2: Java players can join but Bedrock players cannot

This can happen because the Java connection and the Bedrock connection use different networking paths.

Check the Bedrock listener separately.

Verify:

- The bridge is running.
- NetherNet or RakNet is configured correctly.
- The required ports are available.
- The Bedrock client version is supported.

## Problem 3: The server does not appear in the Bedrock server list

Possible causes:

- TCP signaling is unavailable.
- The address or port is incorrect.
- The bridge is not running.
- The server is using a transport not supported by the client.

For NetherNet, the built-in signaling port must be reachable over TCP.

Check the console and networking configuration.

## Problem 4: The server appears, but joining fails

A successful signaling step does not guarantee that gameplay traffic can connect.

Check:

- The required UDP connection.
- Any separate `webrtc-port`.
- Whether the port is allocated and reachable.
- The bridge's startup messages.

## Problem 5: The server description or player count does not appear correctly

Some supported Bedrock client versions may still retrieve server-list information using RakNet.

If the installed bridge documentation recommends both transports for the client version you support, configure combined mode and provide the necessary additional UDP port.

## Problem 6: BaoHost tells me to share the Java and Bedrock ports

This instruction may be appropriate for particular configurations, but it should not be applied blindly to built-in NetherNet signaling.

Read the current hosting instructions.

If the Java port is already occupied by the Java server's TCP listener, a separate TCP listener cannot ordinarily bind to that same endpoint.

Ask BaoHost which NetherNet signaling arrangement it supports.

## Problem 7: An error says the ports for RakNet and NetherNet must be different

When using `transport: both`, check whether `webrtc-port` is different from `port`.

The two transports require separate UDP ports in combined mode.

## Problem 8: Java players can join, but Bedrock players have the wrong address

If the setup uses external signaling, the address given to Bedrock players may differ from the Java address.

Read the bridge's console output and use the exact address and port shown for Bedrock.

Do not assume both editions always use the same address and port.

---

# 16. Frequently Asked Questions

## Q1. Are NetherNet and RakNet for Java or Bedrock?

They are Bedrock transport options.

Java players use the normal Java Edition connection.

## Q2. Does NetherNet replace the Java server?

No.

NetherNet is not a server replacement. It is a Bedrock transport.

A compatible bridge is still required when allowing Bedrock players to join a Java server.

## Q3. Does NetherNet replace the crossplay bridge?

No.

The bridge translates between Bedrock and Java communication. NetherNet describes how the Bedrock client establishes its connection to the bridge.

## Q4. Do I need to change anything on the Java player's computer?

Normally, no.

The server owner configures the crossplay connection. Java players continue joining through the regular multiplayer menu.

## Q5. Should I use RakNet or NetherNet for a new server?

Choose NetherNet when your target Bedrock versions support it and the network setup is ready.

Use both when you need compatible older clients or server-list behavior supported through RakNet.

## Q6. Can RakNet and NetherNet run together?

Yes, with a compatible bridge and the `both` transport setting.

A separate UDP port is required for NetherNet in combined mode.

## Q7. Why does NetherNet need TCP and UDP?

TCP is used for signaling in the built-in setup. Gameplay communication uses WebRTC over UDP.

Both are needed for a normal working connection through that setup.

## Q8. Do Java players use the additional UDP port?

No.

The additional UDP port is part of the Bedrock transport arrangement.

## Q9. Can a server support Java and Bedrock players in the same world?

Yes, when a compatible Java server and crossplay bridge are configured correctly.

The players use different network connections but can participate in the same world.

## Q10. Can all older Bedrock versions connect with RakNet?

No.

Support depends on the client version and the installed bridge. Older versions may also lose support as the software evolves.

## Q11. Will enabling NetherNet fix every Bedrock connection problem?

No.

The client version, bridge version, Java server compatibility, authentication settings, and network ports must all be correct.

## Q12. Which port do I give Bedrock players?

Give them the address and port for the configured Bedrock listener or the connection address displayed by the supported signaling arrangement.

Do not automatically give them the Java server port.

---

# 17. Final Checklist

Before inviting players, verify the following.

## Java Edition

- [ ] The Java server is running.
- [ ] Java players can connect using the normal Java address and port.
- [ ] The server's Java protocol version is compatible with the crossplay setup.

## Bedrock Edition

- [ ] A compatible bridge is installed and running.
- [ ] The chosen transport supports the Bedrock clients you intend to allow.
- [ ] NetherNet is configured when required.
- [ ] RakNet is enabled only when there is a compatibility reason.
- [ ] The required TCP and UDP ports are reachable.
- [ ] The separate UDP port is configured when using both transports.
- [ ] Bedrock players have the correct address and port.

## Hosting

- [ ] BaoHost's port allocations have been checked.
- [ ] The Java server's TCP listener does not conflict with built-in NetherNet signaling.
- [ ] Any external signaling arrangement has been checked.
- [ ] The server has been restarted after configuration changes.
- [ ] Both Java and Bedrock connections have been tested.

---

# 18. Official Resources

| Resource | Link |
|---|---|
| GeyserMC official website | https://geysermc.org/ |
| GeyserMC setup guide | https://geysermc.org/wiki/geyser/setup/ |
| GeyserMC supported versions | https://geysermc.org/wiki/geyser/supported-versions/ |
| Preparing Your Geyser Server for NetherNet | https://geysermc.org/blog/preparing-for-nethernet/ |
| GeyserMC downloads | https://geysermc.org/download |
| BaoHost crossplay tutorial | https://help.baohost.com/articles/geyser-floodgate-crossplay |
| BaoHost Help Center | https://help.baohost.com/ |

---

# Conclusion

RakNet and NetherNet are different ways that Minecraft Bedrock clients establish their network connections.

Java Edition players do not choose either transport. They continue connecting normally to the Java server.

When Bedrock players join a Java server, a compatible bridge handles their connection. RakNet is the traditional Bedrock transport, while NetherNet introduces signaling over TCP before establishing gameplay communication over UDP.

For a new server, plan to support NetherNet. Use both transports when there is a specific reason to support compatible older Bedrock clients or their server-list behavior.

The key is to configure the transport, network ports, and signaling arrangement correctly for your hosting environment.

Always check the current official documentation before applying configuration changes, especially when using a shared Java and Bedrock port on a hosting provider.
