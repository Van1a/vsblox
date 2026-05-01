# VS-BLOX BETA

![Example](https://raw.githubusercontent.com/Van1a/vsblox/refs/heads/main/Images/example.gif)

VS-BLOX is a Roblox scripting bridge that connects your executor to a full IDE environment  including Visual Studio, IntelliJ, or any editor with terminal support  via WebSocket. It enables IDE plugins for a better scripting workflow, real-time previews, and client-side utilities like server-hopping and rejoin commands.

---
## Features

The tool provides support for using plugins in your IDE, allowing your extensions and AI assistants (such as Copilot) to work within your workspace so that you can use a more flexible workflow and increase your coding efficiency.

Using the `run` command will give you output from your code in real-time, as the system will intercept ``hookfunction()`` the print function (which normally provides output in the terminal) and send back all of your results, including errors, directly to your terminal. All of this processing occurs in "live" mode, so you will have a very responsive experience while developing.

You can also call both internal APIs and external APIs simultaneously. Normally, you would only be able to call the `:GetProductInfoAsync()` method (which is unique to Roblox) within the Roblox environment; however, when you connect VS Code to Roblox, you will be able to access this method regardless of where you are coding and can expect to receive a standard value back.

The tool also provides you with the capability of accessing external APIs. For example, you can access the Roblox API and make requests to it, just as if you were working with standard client-side requests. To do this, you may need to have some experience in more than one programming language since the server runs on a Node.js development environment. However, the server can communicate between all programming languages, giving you the ability to create flexible and scalable integrations.

Lastly, you will be able to access tools designed to aid in controlling Roblox. A good example of this is the ability to quickly open the console

---

## Contributing

We welcome all contributions! Whether it's bug fixes, new features, or performance improvements, your help makes VS-BLOX faster, safer, and more stable. See our [contribution guide](<URL>) to get started.

---

## Requirements

You need two environments set up correctly for VS-BLOX to work:

1. **An IDE with a built-in terminal**  This runs the WebSocket server that acts as the bridge between your editor and Roblox.
2. **A Roblox executor**  Your executor must support the following [UNC](https://github.com/unified-naming-convention/NamingStandard) features:
   - `WebSocket`
   - `cloneref()`
   - `newcclosure()`
   - `hookfunction()`
   - `FileSystem`

   Most modern executors already support these, so you usually won't need to configure anything extra.

---

## Setup: Terminal (Server Side)

**Step 1  Clone the repository**

```bash
git clone https://github.com/Van1a/vsblox.git
```

**Step 2  Navigate into the project directory**

```bash
cd vsblox
```

**Step 3  Install dependencies**

```bash
npm install
```

**Step 4  Start the WebSocket server**

```bash
node server
```

If everything is working, you'll see a banner in your terminal displaying your active WebSocket connection address.

![Example of server running](https://raw.githubusercontent.com/Van1a/vsblox/refs/heads/main/Images/Running.png)

> If you followed all the steps and it still doesn't work, reach out to the owner on [Discord for support](https://discord.gg/pkc2ASf9Kb).

---

## Setup: Roblox (Client Side)

Once the server is running, configure the client in your executor. Choose one of the two connection methods below:

### Localhost Connection *(same device)*

Use this when the server and Roblox are running on the same machine. No external IP needed.

```lua
getgenv().WebSocketProvider = createConnection({
    IpAddress = "localhost",
    Port = 3000
})

loadstring(HttpGet("url"))()
```

### LAN Connection *(different devices)*

Use this to connect from a separate device (e.g., mobile to desktop). The server must be running on the machine whose IP address you provide.

```lua
getgenv().WebSocketProvider = createConnection({
    IpAddress = "123.456.789.102",
    Port = 3000
})

loadstring(HttpGet("url"))()
```

## Connection
Now, once you’ve determined where you want to connect, the only thing left to do is run the code. To verify that the connection is successful, you can check the in-game console by pressing F9 ( mobile /console ), or you can look at the terminal where the server is running. If everything is working correctly, it will display a message like ``Client connected``.

### COMMAND
A built-in command designed to interact directly with the system or Roblox environment through the terminal, enabling users to execute actions, trigger functions, and control certain operations efficiently from a command-line interface.

---
### SYSTEM COMMAND
A System Command is a type of command that allows interaction with the server or console, enabling users to execute actions, manage processes, and control system-level or runtime operations directly through the command interface.

| Command | Parameter | Description                              |
|---------|-----------|------------------------------------------|
| change  | path      | Sets the default script file (main.lua) path |
| run     | —         | Executes the code inside main.lua        |
| close   | —         | Closes all active client connections     |
| cls     | —         | Clears the console output                |

### ROBLOX CONTROLLER COMMAND
A Roblox Controller is a built-in system feature that allows predefined functions to be executed automatically, enabling users to perform actions or trigger behaviors without manually writing code.

| Command | Parameter | Function                                                      |
|---------|-----------|---------------------------------------------------------------|
| console | —         | Opens the developer console without using in-game hotkeys     |
| kick    | —         | Disconnects your Roblox client from the current session       |
| rejoin  | —         | Reconnects you to the same server instance                    |
| lowhop  | —         | Switches to a server with the lowest player count             |
| hop     | —         | Teleports you to a different server instance                  |

### Want to request another command? Join the Discord server.
