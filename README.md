# NiceHash Excavator

If you are looking for an easy to use miner with automatic overclocks and fan management, then check out [NiceHash QuickMiner](https://github.com/nicehash/NiceHashQuickMiner) which is a wrapper for Excavator and handles everything automatically so you don't have to.

Excavator is GPU miner by NiceHash for mining various altcoins on [NiceHash.com](https://www.nicehash.com). Hashing speed is comparable to other miners, but it does NOT have any devfee and it comes from a trusted source, completely made by NiceHash developers (we put our signature on final release versions). If you are skeptical towards other closed source miners, or if your PC contains sensitive information, wallet keys and so on, using Excavator (or NiceHash QuickMiner) is prefered way as you do not have to worry anything to be stolen from your PC. It can be used only on NiceHash.

Supported OS:
- Windows 10 64-bit

Supported hardware:
- NVIDIA GeForce GTX 1000 series with minimal 6GB of RAM (Desktop editions)
- NVIDIA GeForce RTX 2000 series with minimal 6GB of RAM (Desktop editions)
- NVIDIA GeForce RTX 3000 series with minimal 6GB of RAM (Desktop editions)

Needed drivers:
- NVIDIA GeForce Game driver 457.xx or higher is required

**WARNING!!! Excavator is a proprietary software by NiceHash and has a special [EULA](excavator-EULA.txt).
YOU ARE NOT ALLOWED TO REDISTRIBUTE IT!**

# Where to get and how to Use Excavator?

There are three possible ways to use Excavator:
1. It is included with [NiceHash Miner](https://www.github.com/nicehash/NiceHashMiner) - just install it and make sure to enable Excavator plugin. Also update to the latest version of plugin.
2. Using it with it's own wrapper called [NiceHash QuickMiner](https://github.com/nicehash/NiceHashQuickMiner). The idea is a simple yet strong (support for overclocking), lightweight Windows 10 miner which does not require anything else to be installed, is super quick to establish and start mining (no time wasted for benchmarking), but it does not do any algorithm switching. If you need to setup mining within one minute on some rig, then this is the best way to go.
3. Be master of your own, using standalone version making your own command scripts: https://github.com/nicehash/excavator/releases

NVIDIA display driver 457.xx or more recent is required. CUDA devices with SM 6.0 (Pascal, 1xxx series) and higher are supported.

From version 1.6.1c Excavator supports only NiceHash stratums. Stratum servers are available at nhmp-ssl.LOCATION.nicehash.com:443 (LOCATION: eu, usa). The same stratum url is used for all algorithms.

**ADVANCED** There are two methods to use Excavator. Both rely on API commands you can find in [API section](/api).

1. Using API port or HTTP API; for that, you need an application that will pass commands to the Excavator. We do not provide any such application (except [web example](/web)), nor there is any public source code available (yet).

   The API works over standard TCP port and is JSON-message based with '\n' terminated messages. Do note that once you build up such application, you virtually have no limits anymore. You can truly optimize your mining to the max; you can launch various algorithms (at the same time), you can randomly assign workers (turn devices on off), do dual/triple mining, algorithm switching, adjusting TDPs, core or memory clock and fan speeds. Additionally to that, you can also read various GPU parameters and algorithm speeds reached by GPUs.

   Default API bind port is 3456, but you can change it with '-p' command line parameter.

   HTTP API is disabled by default. You can enable it by configuring [command line parameters](#cmdline).

2. Using start-up commanding file. See example [default_command_file.json](default_command_file.json).

   File contains a JSON array of all actions that would happen during runtime of Excavator. Each array item has two mandatory fields and one optional. Mandatory is 'time' which tells you after how many seconds since start of Excavator commands should execute and 'commands' which is a JSON array of commands you can find in [API section](/api).

   Optionally you can specify 'loop' which repeat commands every 'loop' seconds. When creating algorithms and workers, note that IDs of returned objects always  run from 0 and on, so first algorithm always has ID 0, second 1 etc.

   You will want to figure out ID of each card; use telnet to connect to Excavator then send command
   > {"id":1,"method":"device.list","params":[]}

   to retreive all available devices and their IDs.

   After you have your commanding file ready, use '-c' command line switch to provide file name when starting Excavator.

   We suggest using [excavator+web+restart_script.bat](excavator+web+restart_script.bat) that automatically launches web browser displaying status and has a restart script to put Excavator back on if it crashes.

Excavator also supports configuring console logging level and file logging level. Level '0' means full detail logging, level '6' means no logging. By default console logging is set to '2', file logging set to '6'. You can change file logging with '-f' and console logging with '-d' command line parameters.

To get details about specific algorithms that are available in Excavator, check [NVIDIA information](/nvidia).

# <a name="cmdline"></a> Command Line Parameters

Parameter | Range | Description | Default
-----------------|----------|----------|---------
-h | none | Displays help; details about all supported command line parameters |
-p | 0-65535 | API bind port; set to 0 to disable API | 3456
-i | local IP | API bind IP | 127.0.0.1
-wp | 0-65535 | HTTP API bind port | 0
-wi | local IP | HTTP API bind IP | 127.0.0.1
-wa | string | HTTP API authorization token |
-wl | string | HTTP API path to index.html file | web\ (windows), web/ (linux)
-d | 0-6 | Console log level | 2
-f | 0-6 | File log level | 6
-fn | file name | Log file | log_$timestamp.log
-c | file name | Use commanding file |
-m | none | Allow running multiple instances of Excavator |
-t | 0, 1 | 0 = production, 1 = use test.nicehash.com | 0
-ql | eu, usa | QuickMiner location | eu
-qu | string | QuickMiner user name |
-qc | none | QuickMiner enable CPU mining |
-qm | none | Minimize when starting |
-qx | none | Suppress QuickMiner text |


# Additional Notices

WARNING! Excavator supports overclocking. Use overclocking at your own risk. OVERCLOCKING MAY PERMANENTLY DAMAGE YOUR COMPUTER HARDWARE!

The algorithm names are case sensitive. 
