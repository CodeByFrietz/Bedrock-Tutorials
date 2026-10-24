# Minecraft Server Errors and Troubleshooting Guide

**BaoHost | Minecraft Java Edition | Minecraft Bedrock Edition | Paper | Fabric | Forge | NeoForge | GeyserMC | Server Administration**

A comprehensive guide explaining common Minecraft server errors, what causes them, how to diagnose them, and how to fix them safely.

This guide covers:

- `Out of memory: true` and `Out of memory: false`
- Exit codes `1`, `128`, `137`, and `143`
- Minecraft Java Edition `getsockopt` errors
- Connection timed out
- Connection refused
- Connection reset
- Unknown host
- Failed to verify username
- Invalid session
- Outdated client and outdated server
- Unsupported Java versions
- Failed to bind to port
- Server startup failures
- Plugin and mod errors
- Missing dependencies
- World and chunk errors
- Watchdog errors and server lag
- Disk space problems
- File upload errors
- BaoHost panel and power-button problems
- Bedrock connection problems
- Crossplay-related errors
- How to read logs and request support

**Documentation checked:** October 24, 2026.

Error messages can vary depending on the Minecraft version, server software, operating system, hosting provider, and installed plugins or mods. The steps below are diagnostic guidelines, not a guarantee that every error has one specific cause.

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Before Fixing Any Error](#2-before-fixing-any-error)
3. [Understanding BaoHost's Out of Memory Indicator](#3-understanding-baohosts-out-of-memory-indicator)
4. [Exit Code 137 — Out of Memory or Forced Termination](#4-exit-code-137--out-of-memory-or-forced-termination)
5. [Exit Code 143 — Server Terminated or Stopped](#5-exit-code-143--server-terminated-or-stopped)
6. [Exit Code 128 — Elytra Daemon Error](#6-exit-code-128--elytra-daemon-error)
7. [Exit Code 1 — General Server Crash](#7-exit-code-1--general-server-crash)
8. [Other Exit Codes and Java Errors](#8-other-exit-codes-and-java-errors)
9. [Java Edition: Getsockopt and Connection Errors](#9-java-edition-getsockopt-and-connection-errors)
10. [Connection Reset and Internal Exception Errors](#10-connection-reset-and-internal-exception-errors)
11. [ReadTimeoutException and Timeouts During Gameplay](#11-readtimeoutexception-and-timeouts-during-gameplay)
12. [Unknown Host and DNS Errors](#12-unknown-host-and-dns-errors)
13. [Authentication and Invalid Session Errors](#13-authentication-and-invalid-session-errors)
14. [Outdated Client and Outdated Server](#14-outdated-client-and-outdated-server)
15. [Failed to Bind to Port](#15-failed-to-bind-to-port)
16. [Java Version and Startup Errors](#16-java-version-and-startup-errors)
17. [Plugin and Mod Errors](#17-plugin-and-mod-errors)
18. [World, Chunk, and Data Errors](#18-world-chunk-and-data-errors)
19. [Server Lag and Watchdog Errors](#19-server-lag-and-watchdog-errors)
20. [Disk Full and Storage Errors](#20-disk-full-and-storage-errors)
21. [File Upload Errors](#21-file-upload-errors)
22. [BaoHost Panel and Installation Errors](#22-baohost-panel-and-installation-errors)
23. [Bedrock and Crossplay Connection Problems](#23-bedrock-and-crossplay-connection-problems)
24. [Server List and MOTD Problems](#24-server-list-and-motd-problems)
25. [A Step-by-Step Troubleshooting Workflow](#25-a-step-by-step-troubleshooting-workflow)
26. [How to Read Minecraft Logs](#26-how-to-read-minecraft-logs)
27. [When to Contact BaoHost Support](#27-when-to-contact-baohost-support)
28. [Frequently Asked Questions](#28-frequently-asked-questions)
29. [Final Troubleshooting Checklist](#29-final-troubleshooting-checklist)
30. [Official References](#30-official-references)

---

# 1. Introduction

Minecraft server errors can look complicated, particularly when the console displays a long Java exception, an exit code, or a message such as `Connection timed out: getsockopt`.

The most important rule is:

**The last error displayed is not always the original cause of the problem.**

For example, a Minecraft server might display:

```text
[Elytra Daemon]: Detected server process in a crashed state!
[Elytra Daemon]: Exit code: 137
[Elytra Daemon]: Out of memory: true
```

This indicates that the process was forcibly terminated and that BaoHost's monitoring system classified the event as an out-of-memory incident.

However, the same server might have previously been suffering from excessive world generation, an overloaded mod, a memory leak, or too many loaded entities.

The exit code helps identify the type of termination, while the earlier console messages and resource statistics help identify the cause.

Similarly, a Minecraft Java Edition player might see:

```text
io.netty.channel.AbstractChannel$AnnotatedConnectException:
Connection timed out: getsockopt
```

This is a connection error experienced by the player. It does not automatically mean the server crashed or ran out of RAM.

To diagnose errors properly, you must separate three different categories:

| Category | Examples | Where to investigate |
|---|---|---|
| Server process errors | Exit code 137, exit code 143, Out of memory | BaoHost console, resource usage, logs |
| Server application errors | Plugin failure, Java version error, world corruption | Server console, `latest.log`, crash reports |
| Player connection errors | Getsockopt, connection refused, connection reset | Server address, ports, network, client, server logs |

This guide explains how to identify which category applies and what to do next.

---

# 2. Before Fixing Any Error

Before changing anything, follow these basic rules.

## Step 1: Check whether the server is actually online

Open the BaoHost panel and look at the server's current status.

If the server is offline or still starting, players may be unable to connect.

Wait until startup completes before asking someone to test the connection.

## Step 2: Check the console

Open the Console tab.

Look at the messages immediately before the error or exit code.

For example:

```text
[Server thread/ERROR]: Could not load plugin
[Server thread/INFO]: Stopping server
[Elytra Daemon]: Exit code: 1
```

The plugin error might explain why the server stopped. The exit code alone cannot identify that plugin.

## Step 3: Open the logs

If the console does not show enough information, open:

```text
logs/latest.log
```

You may also find useful information in:

```text
crash-reports/
```

Not every failure generates a crash report. Some processes are terminated without producing a Java crash report.

BaoHost's crash troubleshooting guide explains how to review Crash Analysis and `latest.log`:

https://help.baohost.com/articles/server-crashing

## Step 4: Check what changed recently

Think about the actions immediately before the issue started.

Examples include:

- Installing a new plugin.
- Updating a mod.
- Changing Minecraft versions.
- Changing the Java runtime.
- Uploading a new world.
- Editing `server.properties`.
- Changing a startup configuration.
- Adding a behavior pack or resource pack.
- Increasing player capacity or world generation.
- Changing the server software.

If the problem started immediately after a change, that change is a useful clue.

## Step 5: Back up before modifying important files

Stop the server before editing its files.

Create a backup of the world and relevant configuration files before performing major troubleshooting.

Do not delete your world, reinstall the server, or remove all plugins simply because an error appears.

The correct fix should be based on the error and supporting evidence.

Paper's official troubleshooting guide recommends stopping the server and creating a backup before making changes:

https://docs.papermc.io/paper/basic-troubleshooting/

---

# 3. Understanding BaoHost's Out of Memory Indicator

BaoHost may display an error report similar to:

```text
[Elytra Daemon]: Exit code: 137
[Elytra Daemon]: Out of memory: true
```

Or:

```text
[Elytra Daemon]: Exit code: 143
[Elytra Daemon]: Out of memory: false
```

These two lines provide different information.

## What does `Out of memory: true` mean?

It means BaoHost's monitoring system classified the event as an out-of-memory incident.

This commonly occurs when the server exceeds its available memory limit and the operating environment terminates the process.

The server may stop during startup, world generation, normal gameplay, or while several players are online.

Common causes include:

- Too many plugins or mods.
- A memory-intensive plugin.
- Excessive world generation.
- Too many loaded chunks.
- Large quantities of entities.
- An add-on that consumes excessive memory.
- A memory leak.
- Insufficient RAM for the workload.

BaoHost's relevant documentation:

https://help.baohost.com/articles/out-of-memory

## What does `Out of memory: false` mean?

It means BaoHost's monitoring system did not classify that particular process termination as an out-of-memory event.

It does **not** prove that your server has unlimited available memory or that memory could not have contributed to a separate problem.

For example, Java can report an internal exception such as:

```text
java.lang.OutOfMemoryError: Java heap space
```

That is a separate piece of evidence and must be investigated even if the hosting panel's indicator says `false`.

Check the console, memory graph, and the exact exception.

## Does `Out of memory: true` always mean I need more RAM?

Not necessarily.

More RAM may help when the server genuinely needs more memory, but excessive resource usage can sometimes be reduced by finding the plugin, mod, or workload causing the problem.

Before upgrading, investigate why memory usage is increasing.

## Does `Out of memory: false` mean everything is fine?

No.

Your server might still be experiencing:

- A Java exception.
- A plugin crash.
- A configuration error.
- A manual or automatic shutdown.
- A hosting-node issue.
- An incompatible Java version.
- A failed port binding.
- A world-loading error.

**Always read the error message preceding the exit code.**

## How to check your allocated RAM on BaoHost

1. Log in to your BaoHost panel.
2. Open your server.
3. Locate the three-dot menu near the top of the panel.
4. Select **My Limitations**.
5. Check the allocated RAM, CPU, and disk space.
6. Compare the limits with the server's reported usage.

Official guide:

https://help.baohost.com/articles/server-specs

---

# 4. Exit Code 137 — Out of Memory or Forced Termination

## What does exit code 137 mean?

On Linux-style systems, process exit codes often use the convention `128 + signal number` when a process is terminated by a signal.

Signal 9 is `SIGKILL`, so:

```text
128 + 9 = 137
```

Exit code 137 commonly indicates that the server process was killed forcefully.

In containerized hosting environments, an out-of-memory kill is a common reason for this exit code.

However, the number alone is not absolute proof that RAM was the cause.

BaoHost's documentation associates exit code 137 with forced termination and, in most cases, insufficient available memory.

Official reference:

https://help.baohost.com/articles/exit-code-137

## Example

```text
[Elytra Daemon]: Detected server process in a crashed state!
[Elytra Daemon]: Exit code: 137
[Elytra Daemon]: Out of memory: true
```

This strongly suggests that you should investigate memory usage.

## Common causes

### 1. Not enough allocated RAM

The server's workload may exceed the memory available under your plan.

### 2. Too many plugins or mods

Some plugins and mods consume significant memory, especially when they load large datasets, maps, entities, or persistent caches.

### 3. Excessive world generation

Generating new terrain can create additional CPU and memory pressure.

This may be especially noticeable when players travel quickly into unexplored areas.

### 4. Too many loaded chunks and entities

Large farms, entity-heavy areas, many players exploring different regions, and other demanding workloads can increase resource consumption.

### 5. A memory leak

A plugin or mod might retain objects that are no longer needed, causing memory usage to grow over time.

### 6. Incorrect Java memory settings

The Java maximum heap size might be configured too close to the container's total memory limit.

Java also needs memory outside its heap for class metadata, thread stacks, native allocations, and other runtime requirements.

Paper's documentation warns that the JVM can use more memory than its configured heap size. The container limit must leave room for this additional usage.

Reference:

https://docs.papermc.io/paper/basic-troubleshooting/

## How to fix exit code 137

### Step 1: Check the resource graph

Open the BaoHost panel and inspect RAM usage before the crash.

If usage repeatedly reaches the limit before the process stops, memory pressure is a likely cause.

### Step 2: Identify recent plugin or mod changes

If you recently added something, review its requirements.

With the server stopped, temporarily disable the suspected plugin or mod after creating a backup.

If the problem disappears, investigate that component.

### Step 3: Reduce unnecessary workload

Possible actions include:

- Removing unused plugins.
- Removing incompatible or unnecessary mods.
- Reducing entity-heavy farms.
- Avoiding excessive numbers of simultaneously loaded chunks.
- Reviewing demanding scripts and add-ons.
- Checking for known memory leaks.

Do not remove important dependencies without checking which plugins rely on them.

### Step 4: Review world-generation activity

If the crash occurs during exploration or chunk generation, consider pre-generating chunks with a compatible tool such as Chunky.

Official project:

https://modrinth.com/plugin/chunky

Pre-generation can help reduce repeated live world-generation work, but it is not a guaranteed RAM fix. Large pre-generation jobs can themselves consume substantial CPU and resources.

Start with a small area and monitor usage.

### Step 5: Check Java memory configuration

On a self-managed server, `-Xmx` controls the maximum Java heap size.

On a managed hosting platform, do not blindly replace the startup command or set `-Xmx` equal to the entire RAM allocation.

Leave sufficient memory for the Java runtime and the operating environment.

Follow the hosting provider's instructions for Java memory settings.

### Step 6: Consider additional RAM if necessary

If the server still exceeds its limits after reasonable optimization, it may need more resources.

Check your current plan and available upgrade options.

### Step 7: Contact support if the cause remains unclear

Provide the exit code, the memory graph, the full console log, and the time of the incident.

### What not to do

Do not immediately:

- Delete the world.
- Reinstall the entire server.
- Remove every plugin.
- Increase random Java memory arguments.
- Assume a restart permanently fixes the problem.

A restart might temporarily reduce usage without fixing the underlying cause.

---

# 5. Exit Code 143 — Server Terminated or Stopped

## What does exit code 143 mean?

Under the common Linux exit-status convention:

```text
128 + 15 = 143
```

Signal 15 is `SIGTERM`, a termination request.

Exit code 143 often means that the server process received a request to shut down.

It does not normally indicate an out-of-memory kill.

Official BaoHost reference:

https://help.baohost.com/articles/exit-code-143

## Example

```text
[Server thread/INFO]: Stopping server
[Server thread/INFO]: Saving worlds
[Elytra Daemon]: Exit code: 143
[Elytra Daemon]: Out of memory: false
```

If you deliberately pressed Stop or Restart, this can be normal.

The server was told to terminate, and the process exited.

## Common causes

- You clicked Stop.
- You clicked Restart.
- Someone with access to the panel stopped the server.
- An automatic restart was triggered.
- A scheduled task stopped the server.
- The hosting environment terminated the process.
- A container restart occurred.
- The hosting node underwent maintenance.
- Another system process requested a shutdown.

## How to troubleshoot exit code 143

### Step 1: Determine whether the shutdown was intentional

Ask yourself:

- Did I press Stop?
- Did I press Restart?
- Did someone else access the panel?
- Was the server updating?
- Was a scheduled task running?

If the answer is yes, the exit code may be normal.

### Step 2: Check the preceding console messages

Look for messages such as:

```text
Stopping server
Saving worlds
Stopping server thread
Server shutdown
```

These can indicate a normal shutdown.

### Step 3: Check scheduled tasks

Inspect any scheduled tasks or automated restart features.

Make sure nothing is unintentionally stopping the server.

### Step 4: Check recent changes

If exit code 143 started unexpectedly, investigate what changed.

Examples:

- Plugin update.
- Mod update.
- Server software change.
- Java version change.
- Startup configuration change.
- Server configuration change.

### Step 5: Check resource usage anyway

Although code 143 does not normally mean out of memory, review memory, CPU, disk usage, and the console if the server stopped without your involvement.

If the panel reports `Out of memory: true`, investigate that evidence separately.

### Step 6: Contact support if the server stops by itself

If the server repeatedly shuts down without anyone requesting it, provide the full console log and the exact time of the shutdown.

## What not to do

Do not automatically reinstall the server, delete the world, or upgrade RAM because of code 143 alone.

**The key is to identify who or what requested the shutdown.**

---

# 6. Exit Code 128 — Elytra Daemon Error

BaoHost has a specific support article for exit code 128 in its Elytra Daemon.

Reference:

https://help.baohost.com/articles/exit-code-128

## Example

```text
[Elytra Daemon]: Detected server process in a crashed state!
[Elytra Daemon]: Exit code: 128
[Elytra Daemon]: Out of memory: false
```

## What can cause this on BaoHost?

BaoHost's support documentation associates this panel-specific error with possible causes including:

- A hosting-node outage.
- Node maintenance.
- A bug or corruption in server files.

However, an exit code of 128 by itself is not a universal diagnosis across every operating system or process manager.

Do not assume that all exit code 128 errors everywhere have the same cause.

## How to troubleshoot it

### Step 1: Check for a hosting outage

Look for BaoHost announcements about your node or maintenance.

### Step 2: Inspect the console

Read the messages before the exit code.

Look for file errors, startup failures, or indications that the hosting environment could not start the server.

### Step 3: Check recent file changes

Think about whether files were deleted, overwritten, or replaced.

### Step 4: Back up your files

Create a backup before attempting a repair or reinstall.

### Step 5: Avoid reinstalling as the first step

BaoHost documents reinstalling as a possible remedy when server files are corrupted or missing, but reinstalling with a full file wipe can delete everything.

Do not wipe the server unless you have backed up the world, plugins, configuration, and other required files.

### Step 6: Contact support

If the server is fresh, the console does not identify an error, or the problem persists, ask BaoHost to check the node and server files.

Provide the server ID, exit code, and full console log.

---

# 7. Exit Code 1 — General Server Crash

## What does exit code 1 mean?

Exit code 1 is a general non-zero process exit status.

It does not identify one specific Minecraft problem.

The server may have failed because of a configuration error, incompatible plugin, missing file, Java version mismatch, or another startup problem.

BaoHost has a support article covering its exit code 1 reports:

https://help.baohost.com/articles/exit-code-1

## Example

```text
[Elytra Daemon]: Detected server process in a crashed state!
[Elytra Daemon]: Exit code: 1
[Elytra Daemon]: Out of memory: false
```

## Common causes

- An incompatible plugin.
- An incompatible mod.
- A missing dependency.
- A malformed configuration file.
- A corrupted or missing server file.
- An incorrect Java runtime.
- An invalid startup configuration.
- A hosting-node problem.

## How to fix exit code 1

### Step 1: Read the log before the exit code

Look for the first meaningful error.

Examples:

```text
UnsupportedClassVersionError
```

This often points to an incompatible Java runtime.

```text
Could not load plugin
```

This points toward plugin compatibility, dependency, or loading problems.

```text
Invalid or corrupt jarfile
```

This suggests that a JAR file may be damaged or invalid.

### Step 2: Check recent changes

If the server worked before installing a plugin or mod, investigate that change first.

### Step 3: Check compatibility

Confirm that the plugin or mod supports your:

- Minecraft version.
- Server software.
- Java runtime.
- Mod loader, when applicable.

### Step 4: Review configuration files

Look for malformed YAML, invalid JSON, missing required settings, or incorrect file paths.

Do not replace every configuration file with a random example from the internet.

### Step 5: Check Java requirements

Choose the Java runtime required by the exact Minecraft and server-software version.

### Step 6: Restore from a backup if necessary

If the problem began after a major configuration change, consider restoring the affected file from a known-good backup.

### Step 7: Contact support if the error remains unclear

Provide the full startup log and the first meaningful exception, not just the exit code.

---

# 8. Other Exit Codes and Java Errors

The following table is a quick reference. Interpret codes in context, particularly on a managed hosting platform.

| Error or code | Typical interpretation | What to check first |
|---|---|---|
| `0` | Normal successful process exit | Was the server intentionally stopped? |
| `1` | General application error | Console exception, plugin, Java version, configuration |
| `128` | Ambiguous by itself; BaoHost documents specific Elytra Daemon cases | Node status, startup log, server files |
| `137` | Often a process killed by SIGKILL; memory pressure is a common cause | RAM usage and `Out of memory` indicator |
| `143` | Often a process terminated by SIGTERM | Stop/restart actions, scheduled tasks, host events |
| `UnsupportedClassVersionError` | Java runtime is too old for the compiled server or plugin | Java runtime selection |
| `OutOfMemoryError` | Java could not allocate required memory | Exact exception, heap/native memory, resource limits |
| `NoClassDefFoundError` | Required class missing at runtime | Missing dependency, wrong plugin build, incompatible libraries |
| `ClassNotFoundException` | A requested class cannot be found | File paths, dependencies, software version |
| `ExceptionInInitializerError` | A class failed while being initialized | Nested cause or `Caused by` lines |
| `StackOverflowError` | Call stack exhausted, possibly due to recursion | Plugin/mod code and nested error trace |

**Important:** An exit code is a clue, not a complete crash report. Always identify the first meaningful error in the console.

---

# 9. Java Edition: Getsockopt and Connection Errors

This section covers the connection errors players commonly see when joining a Minecraft Java Edition server.

The word `getsockopt` is not usually the real cause of the failure.

It is part of a low-level networking error message.

Pay attention to the words immediately before it:

- `Connection timed out`
- `Connection refused`
- `Connection reset`

These messages indicate different types of connection failures.

## 9.1. Connection timed out: getsockopt

Example:

```text
io.netty.channel.AbstractChannel$AnnotatedConnectException:
Connection timed out: getsockopt
```

### What does it mean?

The client attempted to connect to the address and port, but the connection did not complete within the expected time.

Possible causes include:

- The server is offline.
- The address is incorrect.
- The port is incorrect.
- The necessary network traffic is blocked or dropped.
- The hosting provider is experiencing a network problem.
- The player is using an incorrect hostname.
- The player's network is preventing the connection.

This error alone cannot identify which cause applies.

### How to fix it

#### Step 1: Verify that the server is online

Open BaoHost and check the server status.

If the server is still starting or is offline, wait until it finishes starting.

#### Step 2: Copy the correct address

Open your BaoHost panel and copy the exact server address and port.

Do not guess the port.

#### Step 3: Make sure the player uses the correct address format

For example:

```text
play.example.com:25565
```

This is an example address.

Use the actual address displayed by the hosting panel.

Do not add `https://` in front of a Minecraft server address.

#### Step 4: Check whether the server completed startup

The server should have completed its startup process before players connect.

If it has crashed or stopped starting, resolve that issue first.

#### Step 5: Check whether other players can connect

If nobody can join, investigate the server status, address, port, and host network.

If only one player cannot connect, investigate that player's network or client configuration.

#### Step 6: Try another network

If appropriate, test from another trusted network.

If the connection works elsewhere, the original network, firewall, or routing path may be involved.

#### Step 7: Ask BaoHost to check the network

If the server is online, the address is correct, and multiple players still get timeouts, provide BaoHost with the server address, port, and approximate time of failure.

### Important

Do not immediately delete plugins, change the world, or reinstall the server because of `Connection timed out: getsockopt`.

It is primarily a connection problem, not proof of a corrupted world or an out-of-memory crash.

---

## 9.2. Connection refused: getsockopt

Example:

```text
io.netty.channel.AbstractChannel$AnnotatedConnectException:
Connection refused: getsockopt
```

Another common form is:

```text
Connection refused: no further information
```

### What does it mean?

The connection attempt was actively refused.

A common explanation is that the destination address was reached but no service was accepting connections on that port.

Possible causes include:

- The server is offline.
- The server is still starting.
- The wrong port was entered.
- The server failed to bind to its port.
- A firewall rejected the connection.
- The address points to the wrong service.

### How to fix it

1. Confirm that the server is online.
2. Wait for startup to finish.
3. Copy the correct server address and port.
4. Check the console for `Failed to bind to port`.
5. Verify that the server is listening on the expected address and port.
6. Contact BaoHost if the server is online but the correct port consistently refuses connections.

### Difference between refused and timed out

| Error | General meaning |
|---|---|
| Connection refused | The connection was rejected. A common cause is that nothing is listening on the destination port. |
| Connection timed out | No successful response arrived before the connection timed out. Traffic may be blocked, dropped, or directed to the wrong destination. |

The distinction helps narrow down the investigation, but neither message proves one exact cause.

---

## 9.3. Connection refused: no further information

This is another form of connection refusal.

It commonly occurs when:

- The server is stopped.
- A server is running on another port.
- Startup failed before the listener opened.
- A firewall actively rejects traffic.
- The address points to the wrong server.

Start with the server status, address, port, and console.

Do not reinstall Minecraft as the first step.

---

## 9.4. `io.netty.channel.AbstractChannel$AnnotatedConnectException`

This long class name often appears before the actual connection error.

For example:

```text
io.netty.channel.AbstractChannel$AnnotatedConnectException:
Connection timed out: getsockopt
```

The class name alone does not tell you the complete cause.

Read the remaining exception text.

If the final message says `Connection timed out`, follow the timeout troubleshooting steps.

If it says `Connection refused`, follow the connection-refused steps.

If it shows another message, investigate that specific message instead.

---

# 10. Connection Reset and Internal Exception Errors

A common Minecraft Java Edition error is:

```text
Internal Exception: java.net.SocketException: Connection reset
```

## What does it mean?

The connection was interrupted or reset unexpectedly.

This does not necessarily mean the server crashed.

Possible causes include:

- An unstable network connection.
- The server restarting or disconnecting the player.
- A proxy or network device closing the connection.
- A server stall.
- A plugin or mod problem.
- Version or protocol incompatibility.
- A client-specific networking problem.

The exact cause depends on the server logs and whether other players are affected.

## How to fix it

### Step 1: Determine whether the problem affects everyone

Ask whether other players can stay connected.

If many players disconnect at the same time, investigate the server, host, or shared network path.

If only one player has the problem, investigate that player's connection and client.

### Step 2: Check server logs

Look for messages corresponding to the time the player disconnected.

Check for server restarts, plugin errors, high server load, or repeated network errors.

### Step 3: Check the Minecraft version

Make sure the player's client version is supported by the server.

If the server uses mods, confirm that the player has the required compatible modpack.

### Step 4: Temporarily test without recently added plugins or mods

Only do this after backing up the server and ensuring the test does not break important dependencies.

If the error began after adding a plugin or mod, investigate that component first.

### Step 5: Test the player's network

Try another trusted network where practical.

If the problem only happens on one network, the network path, router, or firewall may be involved.

### Step 6: Check whether the server is lagging

If chunks stop loading or the server becomes unresponsive before the disconnect, review server performance.

A reset can be a symptom of another issue rather than the root cause.

---

# 11. ReadTimeoutException and Timeouts During Gameplay

Example:

```text
Internal Exception: io.netty.handler.timeout.ReadTimeoutException
```

## What does it mean?

The connection did not receive the expected data within the allowed time.

This can occur during the initial connection or later in gameplay.

It does not automatically mean the player's internet is slow, nor does it automatically mean the server has run out of RAM.

## Possible causes

- A temporary network interruption.
- A server that is not responding promptly.
- A severely overloaded server.
- A plugin blocking or stalling important server operations.
- A connection problem involving a proxy.
- A mod or protocol incompatibility.

## How to troubleshoot

1. Check whether the server is online and responsive.
2. Ask whether multiple players are experiencing the issue.
3. Check the console at the time of disconnection.
4. Review server lag and resource usage.
5. Check the required Minecraft version and modpack.
6. If only one player is affected, test their client and network separately.

If the error happens when the world stops loading, investigate server performance rather than changing random network settings.

---

# 12. Unknown Host and DNS Errors

Common examples include:

```text
Unknown host
```

```text
java.net.UnknownHostException
```

```text
Can't resolve hostname
```

## What does it mean?

Minecraft could not resolve the server's hostname into a usable network address.

This is different from a connection timeout.

A timeout generally means a connection did not complete. An unknown-host error means the hostname could not be resolved correctly.

## Common causes

- Typing the address incorrectly.
- Using an outdated custom hostname.
- DNS records not being configured correctly.
- A recently changed DNS record not being available everywhere yet.
- Entering a URL instead of a server hostname.
- Using a hostname that does not exist.

## How to fix it

### Step 1: Copy the server address

Use the address shown in BaoHost.

Check every character.

### Step 2: Remove website prefixes

Minecraft server addresses do not normally include:

```text
https://
```

or:

```text
http://
```

Enter the hostname itself.

### Step 3: Check the port separately

If a port is required, enter it using the server address format supported by the Minecraft multiplayer menu.

For Java, a manually specified port is commonly entered as:

```text
play.example.com:25565
```

This is only an example.

### Step 4: Check custom DNS

If you configured a custom domain or hostname, check its DNS records and target.

### Step 5: Wait for recent DNS changes

If you just changed your DNS settings, allow time for the change to propagate.

### Step 6: Contact the provider if the hostname remains unresolved

Provide the hostname and explain whether the problem affects all players or only one network.

---

# 13. Authentication and Invalid Session Errors

Connection problems are not always caused by network ports.

Minecraft Java Edition also needs to authenticate accounts when connecting to servers that require normal online authentication.

## 13.1. Invalid session

A player may see a message indicating that their session is invalid.

Possible causes include:

- The launcher session expired.
- The player signed out.
- Authentication information is stale.
- Account authentication failed.

### How to fix it

1. Save any single-player progress.
2. Close Minecraft.
3. Sign out of the official Minecraft Launcher account.
4. Sign back in.
5. Launch the correct Minecraft profile.
6. Try connecting again.

If the error affects many players simultaneously, check for an authentication-service issue rather than changing the server's port or deleting the world.

## 13.2. Failed to verify username

An error such as:

```text
Failed to verify username!
```

may appear when the server cannot verify the player's account session.

Possible causes include:

- Invalid login session.
- Authentication-service problems.
- Incorrect server authentication configuration.
- A connection issue preventing normal authentication.

### How to troubleshoot

1. Sign out and back into the official launcher.
2. Confirm that the account can launch the intended Minecraft edition.
3. Try again after confirming the server is online.
4. Check whether other players have the same problem.
5. If multiple players are affected, investigate authentication services and the server's configuration.

Do not disable authentication or remove security protections simply to bypass an authentication error.

## 13.3. Authentication service unavailable

If the launcher or server cannot reach the required authentication services, login may fail.

Check the official Minecraft support resources and whether the issue affects other players.

Official Minecraft Help:

https://help.minecraft.net/

---

# 14. Outdated Client and Outdated Server

Common messages include:

```text
Outdated client! Please use ...
```

```text
Outdated server! I'm still on ...
```

```text
Incompatible client!
```

## What do they mean?

The client and server are using incompatible Minecraft protocol versions.

For example:

- A client on a newer version may be unable to join an older server.
- An older client may be unable to join a newer server.

The version mentioned in the message can help identify which version needs to be used.

## How to fix it

### Option A: Use the server's version

In the Minecraft Java Launcher:

1. Open the Installations section.
2. Create or edit an installation.
3. Select the Minecraft version supported by the server.
4. Launch that installation.
5. Join again.

Only download or select versions through legitimate sources.

### Option B: Update the server

If the server owner wants everyone to use the latest compatible version, update the server software using the provider's supported process.

Back up the world and check plugin or mod compatibility before updating.

### Option C: Use a compatible protocol bridge

Java plugins such as ViaVersion can support certain additional Java client versions.

However, ViaVersion does not make every version combination compatible.

The required plugin, supported client versions, and server version must all be compatible.

Official project:

https://viaversion.com/

## Important for Bedrock crossplay

Bedrock clients and Java clients use different protocols.

A Java protocol compatibility plugin does not replace the software needed to bridge Bedrock and Java.

For crossplay, verify the compatibility requirements of the actual bridge you use.

---

# 15. Failed to Bind to Port

Example:

```text
FAILED TO BIND TO PORT
```

Or:

```text
java.net.BindException: Address already in use
```

## What does it mean?

The server could not open the requested network endpoint.

Possible causes include:

- Another server process already occupies the port.
- The port allocation is incorrect.
- The configured address is invalid.
- Another service is using the same TCP port.
- The hosting environment does not permit that port arrangement.

## How to fix it on BaoHost

1. Check the server console.
2. Confirm that you do not have an overlapping running process.
3. Verify the port assigned by BaoHost.
4. Avoid changing the server's port randomly.
5. Contact BaoHost if the allocation appears incorrect.

## What about `server-ip` in `server.properties`?

On a self-managed server, the `server-ip` property controls which network interface Minecraft binds to.

It is not a field for entering the public IP address of your server.

Paper's documentation notes that it should generally be left empty unless a specific binding configuration is needed.

For a managed hosting server, follow the hosting provider's guidance instead of editing the address arbitrarily.

Official Paper reference:

https://docs.papermc.io/paper/basic-troubleshooting/

---

# 16. Java Version and Startup Errors

## 16.1. UnsupportedClassVersionError

Example:

```text
java.lang.UnsupportedClassVersionError
```

## What does it mean?

The selected Java runtime is too old to run the server software or plugin.

A server compiled for a newer Java version cannot necessarily run on an older runtime.

## How to fix it

1. Check the Minecraft version.
2. Check the requirements of your server software.
3. Check the requirements of the plugin or mod that failed.
4. Select the appropriate Java runtime in the BaoHost panel.
5. Restart the server.

Do not choose a random Java version. Use the version required by your specific Minecraft server build.

Paper's documentation lists Java runtime compatibility errors as a common startup issue:

https://docs.papermc.io/paper/basic-troubleshooting/

## 16.2. Unable to access jarfile

Example:

```text
Error: Unable to access jarfile server.jar
```

This may indicate that the startup command points to a file that does not exist at the expected location.

It can also occur when the file name or path is incorrect.

### How to fix it

- Check whether the expected file exists.
- Check whether the file was uploaded completely.
- Verify the server software selection.
- Use BaoHost's supported server software options.

BaoHost may restrict uploading custom server JARs directly for security reasons. If so, use the Options tab to choose supported server software instead.

Do not bypass the provider's software restrictions by uploading an unsupported server executable.

## 16.3. Server fails to start after a software change

If the server stops starting after switching software:

1. Check the selected version.
2. Verify the Java runtime.
3. Check plugin and mod compatibility.
4. Read the startup log.
5. Restore the previous working configuration if necessary.

Remember that switching from Paper to Fabric or Forge changes which plugins or mods can run.

---

# 17. Plugin and Mod Errors

Plugins and mods can cause crashes, startup failures, missing features, and unexpected disconnections.

## 17.1. Could not load plugin

Example:

```text
Could not load plugin
```

Possible causes:

- Wrong plugin version.
- Unsupported server software.
- Missing dependency.
- Broken download.
- Invalid plugin metadata.

### Fix

1. Check the plugin's official download page.
2. Confirm the correct build for your Minecraft version.
3. Check its server-software requirements.
4. Check whether it needs another plugin.
5. Review the full console error.

## 17.2. NoClassDefFoundError

Example:

```text
java.lang.NoClassDefFoundError
```

This means the JVM could not find a class needed at runtime.

Possible causes include:

- Missing dependency.
- Incorrect plugin build.
- Incompatible server version.
- A library required by the plugin was not loaded.
- An incompatible combination of plugins.

### Fix

Check the specific missing class and identify which plugin or library requires it.

Do not install random JAR files just because they contain a similar name.

Use the official plugin documentation.

## 17.3. Mod mismatch

Modded clients and servers often need compatible mod loaders and mod versions.

A player may receive a mod mismatch message if the client and server have different required mods.

### Fix

1. Confirm the Minecraft version.
2. Confirm the mod loader.
3. Compare required mods and their versions.
4. Follow the modpack's installation instructions.
5. Check the server log for the exact missing or incompatible component.

Do not assume a Paper plugin will work in a Fabric or Forge `mods` directory.

## 17.4. Missing dependency

Some plugins require library plugins or other components.

If a required dependency is missing, the plugin may fail to load.

Check the error message and install the dependency from its official source if it is supported by your server software.

## 17.5. Plugin conflict

If the server crashes after adding a new plugin:

1. Stop the server.
2. Create a backup.
3. Temporarily disable the new plugin.
4. Restart and test.
5. If the issue disappears, investigate that plugin or its compatibility with other plugins.

If multiple plugins are involved, disable a manageable subset at a time and test systematically.

Do not remove essential dependencies without checking which other plugins rely on them.

Official Paper troubleshooting:

https://docs.papermc.io/paper/basic-troubleshooting/

---

# 18. World, Chunk, and Data Errors

## 18.1. Attempted to load chunk saved with newer version

A typical message is:

```text
Server attempted to load chunk saved with newer version of Minecraft
```

## What does it mean?

The world or chunk data was saved using a newer Minecraft version than the server currently supports.

Minecraft world formats can change between versions.

Opening a newer world on an older server is not a supported downgrade process.

### How to fix it

1. Stop the server.
2. Create a backup of the world.
3. Check which Minecraft version created or last saved the world.
4. Use compatible server software that supports that world format.
5. If you recently downgraded the server, consider returning to the appropriate version.

Do not force the server to ignore world version checks as a routine fix. Doing so may permanently corrupt the world.

Official Paper reference:

https://docs.papermc.io/paper/basic-troubleshooting/

## 18.2. World corruption

Possible symptoms include:

- The server crashes when loading a particular area.
- Chunks fail to load correctly.
- The server stops while loading the world.
- Errors reference region files or chunk data.

### How to troubleshoot

1. Create a backup immediately.
2. Check the crash report and console.
3. Determine whether the crash occurs in a specific world or location.
4. Review recent world conversions or version changes.
5. Test a copy of the world if possible.

Do not delete the entire world because one chunk appears to be corrupted.

## 18.3. The world is missing after a restart

Possible causes:

- The wrong world directory is selected.
- The `level-name` is incorrect.
- The upload was incomplete.
- The world was extracted into an extra nested folder.
- The server is using a different world folder than expected.

Check the world path and the server's configuration before replacing anything.

## 18.4. Missing items, blocks, or entities after a conversion

If a world has been converted between Java and Bedrock, some data may not have equivalent representations.

Custom items, entities, experimental features, and add-ons may not convert correctly.

This is not necessarily an out-of-memory problem or a hosting failure.

Check the conversion tool's limitations and keep the original world as a backup.

---

# 19. Server Lag and Watchdog Errors

## 19.1. Can't keep up! Is the server overloaded?

Example:

```text
Can't keep up! Is the server overloaded?
```

## What does it mean?

The server is taking too long to process its scheduled game ticks.

Possible causes include:

- CPU limitations.
- Heavy world generation.
- Too many entities.
- Redstone-heavy areas.
- Expensive plugin tasks.
- Slow storage operations.
- Large numbers of active players or chunks.

This is not automatically an out-of-memory error.

### How to troubleshoot

1. Check server performance and resource graphs.
2. Identify when lag begins.
3. Check whether it happens in a specific world or area.
4. Review demanding plugins and mods.
5. Reduce unnecessary entity-heavy activities.
6. Consider pre-generating chunks where appropriate.
7. Use a profiling tool if the problem is persistent.

Paper's Spark profiler can help diagnose performance bottlenecks.

Official Paper troubleshooting:

https://docs.papermc.io/paper/basic-troubleshooting/

## 19.2. Watchdog dump

Example:

```text
The server has not responded for 10 seconds! Creating thread dump
```

This indicates that the server is not responding quickly enough.

A watchdog dump is a diagnostic clue, not a complete diagnosis.

The main server thread may be blocked by:

- A plugin task.
- Heavy world generation.
- A long-running operation.
- Excessive entity processing.
- Slow storage.
- Another underlying performance problem.

### How to troubleshoot

1. Read the thread dump.
2. Look for the first relevant stack frames.
3. Check whether a plugin or mod appears in the stalled stack.
4. Review recent changes.
5. Collect a profiling report if necessary.
6. Contact the plugin author or hosting support when the cause is unclear.

Do not automatically assume the watchdog warning means the server ran out of RAM.

## 19.3. Server is lagging even though RAM is available

A server can lag while memory usage is below its limit.

Minecraft's game tick processing depends heavily on CPU performance and the time individual tasks take.

Check CPU usage, plugin activity, world generation, and entities as well as memory.

---

# 20. Disk Full and Storage Errors

BaoHost may display an unexpected error while starting the server if the allocated disk space is full or nearly full.

Example:

```text
[Elytra Daemon]: Checking server disk space usage,
this could take a few seconds...
Error Event: an unexpected error was encountered while handling this request
```

Official BaoHost guide:

https://help.baohost.com/articles/disk-full

## Common causes

- Old world backups.
- Large log files.
- Numerous crash reports.
- Unused plugins or mods.
- Duplicate worlds.
- Large exported world archives.
- Repeated backups consuming storage.

## How to fix it

### Step 1: Check disk usage

In BaoHost, open the three-dot menu and select **My Limitations**.

Check how much storage is used.

### Step 2: Open the Files tab

Identify large files that are no longer needed.

Examples may include:

```text
logs/
crash-reports/
old-backups/
```

The actual directories depend on your setup.

### Step 3: Back up before deleting anything

Do not delete the active world or files you do not recognize.

Keep at least one reliable backup of important worlds and configurations.

### Step 4: Remove unnecessary files

Delete only files that you have confirmed are no longer needed.

### Step 5: Try starting the server again

If storage space was the problem, the server should be able to proceed further.

If the error continues, check the console or ask BaoHost to investigate.

---

# 21. File Upload Errors

You may encounter an error when uploading a world, plugin, or mod through the BaoHost Files tab.

One common problem is trying to upload a folder directly when the file manager expects an archive.

## 21.1. Uploading a folder fails

### How to fix it

1. Compress the folder into a `.zip` archive.
2. Upload the archive.
3. Use the file manager's extraction option.
4. Verify the extracted folder structure.

Alternatively, create the destination folder manually and upload the files individually if appropriate.

## 21.2. File is too large

The upload limit may depend on the server node or panel configuration.

Check BaoHost's current upload limit.

For large world backups, use the host's documented procedure for large-file uploads.

Do not assume every server allocation has the same maximum upload size.

## 21.3. Network error during upload

Possible causes include:

- Interrupted connection.
- File too large.
- Unsupported folder upload.
- Hosting-node maintenance.
- Panel or network issues.

### How to fix it

1. Check whether the file upload completed.
2. Confirm the file size.
3. Compress a folder into a ZIP if necessary.
4. Try again if the host is online and the upload is within the supported limit.
5. Contact support if repeated attempts fail.

Official BaoHost guide:

https://help.baohost.com/articles/network-error-upload

---

# 22. BaoHost Panel and Installation Errors

## 22.1. Power buttons are unresponsive

BaoHost's panel may display a power-event error, or the Start, Stop, and Restart buttons may behave unexpectedly.

Possible causes include:

- Rapidly clicking multiple power buttons.
- A previous action still running.
- Node maintenance.
- A hosting-node outage.

### How to fix it

1. Stop clicking the buttons.
2. Wait for the current operation to finish.
3. Refresh the panel.
4. Try the required power action once.
5. If the problem persists, check BaoHost announcements or contact support.

Official reference:

https://help.baohost.com/articles/power-button-console-issues

## 22.2. Server stuck on installation

Possible causes include:

- Installation is still in progress.
- The server node is overloaded.
- A network issue interrupted the download.
- The hosting node is experiencing an outage.

### How to fix it

1. Allow the installation some time to complete.
2. Refresh the panel and check the current state.
3. Check for hosting-node announcements.
4. Contact support if it remains stuck beyond the provider's stated troubleshooting period.

Official reference:

https://help.baohost.com/articles/stuck-on-installation

## 22.3. Restricted access error — Code 567

BaoHost documents a restricted-access error involving a Tencent or Cloudflare block page.

This is a panel-access problem, not necessarily a Minecraft server crash.

Possible causes can involve web security or access filtering.

### What to do

1. Read the displayed message.
2. Avoid repeatedly refreshing or triggering the block.
3. Check whether the provider has a documented access recovery process.
4. Contact BaoHost support and provide the exact error.

Do not reinstall the Minecraft server to solve a browser access restriction.

Official help center:

https://help.baohost.com/categories/general

## 22.4. Custom server JAR upload is rejected

Some hosting providers restrict custom server JAR uploads for security or compatibility reasons.

If BaoHost rejects a custom server JAR, use the supported software or version options in the panel.

Do not attempt to bypass the provider's restrictions.

Check the software selection options and the provider's current documentation.

---

# 23. Bedrock and Crossplay Connection Problems

This section is for players using Bedrock Edition to join a Java server through a compatible bridge.

## 23.1. Unable to Connect to World

This is a common Bedrock connection message.

Possible causes include:

- Incorrect server address.
- Incorrect Bedrock port.
- The bridge is not running.
- The network does not allow the required Bedrock transport.
- The Bedrock client version is unsupported.
- Authentication failed.
- The server is offline.

### How to fix it

1. Verify the server address.
2. Verify the Bedrock port.
3. Check that the Java server and the bridge have finished starting.
4. Read the bridge's console logs.
5. Confirm the current Bedrock version is supported.
6. Check whether the host supports the required TCP and UDP traffic.
7. Contact the host if the correct port is not reachable.

## 23.2. Java players can join, but Bedrock players cannot

A working Java connection does not guarantee that the Bedrock listener is configured correctly.

Check the crossplay bridge separately.

Verify:

- The bridge is loaded.
- The Bedrock transport is configured correctly.
- The Bedrock port is available.
- Required authentication settings are correct.
- The client version is supported.

## 23.3. Floodgate authentication errors

If you use Geyser and Floodgate, check that both plugins are compatible and configured correctly.

A Bedrock authentication error is not necessarily a Java server RAM problem.

Read the actual console error before changing configuration.

Official project:

https://geysermc.org/

## 23.4. NetherNet or RakNet compatibility errors

If the server recently changed Bedrock transport, verify that the current transport configuration supports the client's version.

NetherNet can require TCP signaling and UDP gameplay traffic. Combined transport setups may require a separate UDP port.

Official setup guide:

https://geysermc.org/wiki/geyser/setup/

Do not assume a normal Java port allocation automatically satisfies every Bedrock transport requirement.

---

# 24. Server List and MOTD Problems

Sometimes the server works when players connect directly, but the multiplayer list displays the wrong description, player count, or status.

## What is MOTD?

MOTD means Message of the Day. It is the description displayed in a server list.

## Possible causes

- The server has not completed startup.
- The status query is using an incorrect address or port.
- A proxy is configured incorrectly.
- The server list is showing cached information.
- A Bedrock transport or status-query compatibility issue exists.
- The server is reachable but the query path is not configured as expected.

## How to troubleshoot

1. Confirm that the server is running.
2. Check the address and port used for the server list.
3. Compare the displayed information with the actual server status.
4. Check whether the issue affects Java, Bedrock, or both.
5. Review any proxy or crossplay configuration.
6. Check the relevant software's documentation.

A missing MOTD or incorrect player count does not necessarily mean that the world is broken.

---

# 25. A Step-by-Step Troubleshooting Workflow

When an error occurs, follow this sequence instead of changing several settings at once.

## Step 1: Identify the exact message

Copy the full error.

For example:

```text
Connection timed out: getsockopt
```

is different from:

```text
Connection refused: getsockopt
```

Record the exit code if one is shown.

## Step 2: Identify who is experiencing the problem

Determine whether:

- The server process has stopped.
- The server is running but players cannot connect.
- Only one player is having trouble.
- Multiple players are affected.
- The BaoHost panel itself is not responding.

This helps narrow down the likely source.

## Step 3: Check the server status

If the server is offline, resolve the startup problem before troubleshooting client-side connection errors.

If the server is online, continue to the next step.

## Step 4: Inspect the relevant logs

Open the console and `logs/latest.log`.

Look for the first meaningful error before the final shutdown message.

Do not rely on the final exit code alone.

## Step 5: Compare with recent changes

Consider what changed immediately before the problem began.

If a new plugin or mod caused the issue, test it carefully after taking a backup.

## Step 6: Check resources

Review:

- RAM.
- CPU.
- Disk storage.
- Server uptime.
- Player count.
- Recent console errors.

Do not assume that every crash is caused by RAM.

## Step 7: Test the simplest possible explanation

For connection errors, check the address and port first.

For startup errors, check the Java runtime and server software.

For memory errors, inspect resource usage and the workload.

For world errors, verify the world format and server version.

## Step 8: Change one thing at a time

If you make multiple unrelated changes simultaneously, it becomes difficult to identify the actual fix.

After each change, restart and test.

## Step 9: Restore a backup if necessary

If the problem began after an irreversible or significant change, consider restoring the last known-good backup.

Keep the original files until the new setup has been verified.

## Step 10: Contact support with evidence

If you cannot identify the cause, provide the log, exact error, time of failure, and relevant server information.

Avoid simply writing "server broken" without any technical details.

---

# 26. How to Read Minecraft Logs

Logs often contain multiple lines of information about the same incident.

Understanding the basic structure makes troubleshooting much easier.

## Example

```text
[Server thread/INFO]: Starting Minecraft server
[Server thread/INFO]: Loading properties
[Server thread/ERROR]: Could not load plugin ExamplePlugin
java.lang.IllegalStateException: Unsupported Minecraft version
    at example.plugin.Main.onEnable(Main.java:42)
[Elytra Daemon]: Exit code: 1
[Elytra Daemon]: Out of memory: false
```

### What this tells us

The plugin did not load because it encountered an unsupported version.

The exit code confirms that the server process ended unsuccessfully, but it is not the original explanation.

The memory indicator says that the daemon did not classify this exit as an out-of-memory incident.

### How to read stack traces

A Java exception may contain lines such as:

```text
java.lang.IllegalStateException: Unsupported Minecraft version
    at example.plugin.Main.onEnable(Main.java:42)
```

The first exception line normally describes the problem being reported.

The `at` lines provide information about where the exception occurred.

Look for plugin names, class names, and `Caused by` sections.

These details can help identify the component that failed.

## Which log files are useful?

| File or location | What it can help identify |
|---|---|
| Console | Current startup errors, shutdown messages, plugin warnings |
| `logs/latest.log` | Detailed record of the latest server run |
| `crash-reports/` | Crash reports when the server generates them |
| Resource graphs | Memory or CPU pressure around a crash |
| Panel status | Whether the process is running or has exited |
| Client error message | Connection or authentication issue experienced by the player |

Not every problem creates a crash report.

If a process is terminated externally, it may stop without producing a complete Java exception.

Paper's official guide provides more information on reading logs, identifying plugin problems, and investigating crashes:

https://docs.papermc.io/paper/basic-troubleshooting/

---

# 27. When to Contact BaoHost Support

Contact support when:

- Your server repeatedly stops without a clear cause.
- The server fails on a fresh installation.
- The hosting node appears to be unavailable.
- Port allocations do not work as expected.
- The panel cannot perform Start, Stop, or Restart actions.
- A disk or memory limit appears inconsistent with the resources allocated.
- The problem continues after reasonable troubleshooting.
- You receive an error indicating that the hosting environment terminated the process.

## What information should you provide?

Use the following template.

```text
Subject: Minecraft Server Error Troubleshooting

Server ID:
Server Software:
Minecraft Version:
Java Version:
RAM Allocation:
CPU Allocation:
Disk Usage:
Exit Code:
Out of Memory: true/false
Approximate Time of Failure:
Number of Players Online:

Exact Error Message:

What I Was Doing When It Happened:

Recent Changes:
- 
- 

Troubleshooting Steps Already Tried:
- 
- 

Console Log:
[Paste the relevant log lines here.]
```

Do not include passwords, authentication keys, private credentials, or other sensitive information in the report.

If you are using a public log-sharing service, inspect the output before sharing it to ensure it does not expose private information.

---

# 28. Frequently Asked Questions

## Q1. Is `Out of memory: false` proof that RAM is not the problem?

No.

It means the host's monitoring system did not classify the specific termination as an out-of-memory event.

Check the Java exception, console, and resource graph.

## Q2. Is exit code 143 always a crash?

No.

It commonly indicates that the process received a termination request. It can be normal when you stop or restart the server.

If the server shuts down unexpectedly, investigate the preceding logs and automation settings.

## Q3. Is exit code 137 always caused by out of memory?

No, although out-of-memory termination is a common cause in hosting environments.

Check the memory indicator, resource usage, and relevant logs.

## Q4. Does exit code 1 mean I need to reinstall my server?

No.

Exit code 1 is a general error. A missing dependency, incompatible plugin, Java version mismatch, or configuration problem may be responsible.

Identify the cause before reinstalling.

## Q5. Does `getsockopt` mean my server's RAM is full?

No.

The meaning depends on the complete error message. `Connection timed out: getsockopt` is a network connection error, not direct proof of memory exhaustion.

## Q6. What is the difference between connection refused and connection timed out?

Connection refused usually means a connection attempt was actively rejected.

Connection timed out means a successful connection was not established before the timeout.

Both may be caused by different networking or server-state problems.

## Q7. My server is online, but nobody can join. What should I check?

Check the address, port, server listener, host network, and console logs.

If all players are affected, investigate the server and host first.

## Q8. Only one player cannot join. Is the server broken?

Not necessarily.

If other players can connect, investigate the affected player's version, address entry, network, firewall, or client configuration.

## Q9. Why does the server use a lot of RAM but not crash?

High RAM usage alone does not prove there is a memory leak.

Java may keep allocated heap memory for future use rather than immediately returning it to the operating system.

Investigate actual out-of-memory errors, garbage collection problems, and resource limits rather than treating the panel's memory percentage alone as a diagnosis.

Paper reference:

https://docs.papermc.io/paper/basic-troubleshooting/

## Q10. Can upgrading RAM fix all server lag?

No.

Server lag can be caused by CPU limitations, long-running plugin tasks, heavy world generation, storage delays, or other issues.

Determine the bottleneck before deciding which resource is insufficient.

## Q11. Should I reinstall immediately if the server crashes?

No.

Reinstallation can delete worlds, plugins, configurations, and other important files.

Back up everything first, then identify the error that caused the failure.

## Q12. Why is the same error happening after every restart?

A restart does not necessarily remove the cause.

If an incompatible plugin, invalid configuration, missing file, or faulty world consistently causes the crash, the same failure can happen again.

Check the exact messages that precede the exit code.

---

# 29. Final Troubleshooting Checklist

Before asking for help, check the following.

## Server status

- [ ] The server is online.
- [ ] Startup completed successfully.
- [ ] The correct Minecraft version is selected.
- [ ] The Java runtime is compatible.
- [ ] The console does not show an unresolved startup error.

## Memory and exit codes

- [ ] RAM usage was checked.
- [ ] `Out of memory: true/false` was recorded.
- [ ] The exit code was recorded.
- [ ] The console output before the exit code was inspected.
- [ ] Recent scheduled restarts and power actions were checked.
- [ ] The memory allocation was not changed blindly.

## Plugins and mods

- [ ] Recently added plugins and mods were checked.
- [ ] Required dependencies are installed.
- [ ] Plugin and mod versions are compatible.
- [ ] Configuration files were reviewed.
- [ ] A backup exists before removing or changing components.

## World and storage

- [ ] The world is in the correct format.
- [ ] The server supports the world version.
- [ ] Important data has been backed up.
- [ ] Disk usage was checked.
- [ ] No unnecessary files were deleted without verification.

## Player connections

- [ ] The server address is correct.
- [ ] The port is correct.
- [ ] The server is accepting connections.
- [ ] The client and server versions are compatible.
- [ ] The exact connection error was identified.
- [ ] The issue was checked against other players and networks.

## Hosting panel

- [ ] BaoHost announcements were checked if a node issue is suspected.
- [ ] Power-button problems were allowed to finish before retrying.
- [ ] The server's allocated resources were verified.
- [ ] Support has the relevant logs and error details if needed.

---

# 30. Official References

The following resources provide additional information about the errors covered in this guide.

| Resource | Link |
|---|---|
| BaoHost Help Center | https://help.baohost.com/ |
| BaoHost: Out of Memory Errors | https://help.baohost.com/articles/out-of-memory |
| BaoHost: Exit Code 137 | https://help.baohost.com/articles/exit-code-137 |
| BaoHost: Exit Code 143 | https://help.baohost.com/articles/exit-code-143 |
| BaoHost: Exit Code 128 | https://help.baohost.com/articles/exit-code-128 |
| BaoHost: Exit Code 1 | https://help.baohost.com/articles/exit-code-1 |
| BaoHost: Server Keeps Crashing | https://help.baohost.com/articles/server-crashing |
| BaoHost: Check Server Specs | https://help.baohost.com/articles/server-specs |
| BaoHost: Disk Full Error | https://help.baohost.com/articles/disk-full |
| BaoHost: Network Error During Upload | https://help.baohost.com/articles/network-error-upload |
| BaoHost: Power Button and Console Issues | https://help.baohost.com/articles/power-button-console-issues |
| BaoHost: Server Stuck on Installation | https://help.baohost.com/articles/stuck-on-installation |
| PaperMC Troubleshooting | https://docs.papermc.io/paper/basic-troubleshooting/ |
| PaperMC Configuration | https://docs.papermc.io/paper/reference/server-properties/ |
| Java OutOfMemoryError Documentation | https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/lang/OutOfMemoryError.html |
| Java Memory Troubleshooting | https://docs.oracle.com/en/java/javase/21/troubleshoot/troubleshooting-memory-leaks.html |
| GNU Bash Exit Status Documentation | https://www.gnu.org/s/bash/manual/html_node/Exit-Status.html |
| Minecraft Help Center | https://help.minecraft.net/ |
| GeyserMC Setup Documentation | https://geysermc.org/wiki/geyser/setup/ |
| GeyserMC Supported Versions | https://geysermc.org/wiki/geyser/supported-versions/ |

---

# Conclusion

Minecraft errors are easier to solve when you identify the exact failure instead of guessing based on one message.

For BaoHost server process errors, start with the exit code, `Out of memory` indicator, console, and resource graph.

For Java Edition connection errors, distinguish timeouts from connection refusals, resets, and hostname-resolution failures.

For crashes, inspect the first meaningful exception in the console or `latest.log`.

For world errors, check the version and format before attempting repairs.

The most important rules are:

1. **Read the logs before changing anything.**
2. **Do not assume every crash is caused by RAM.**
3. **Do not assume `Out of memory: false` proves that no memory problem exists.**
4. **Do not interpret exit code 143 as an automatic out-of-memory crash.**
5. **Do not delete worlds or reinstall the server before creating backups.**
6. **Change one thing at a time and test the result.**
7. **Contact the hosting provider when the evidence points to the node, network, or hosting environment.**

With these steps, server owners and players can identify common Minecraft errors more accurately, avoid unnecessary changes, and provide better information when asking for support.
