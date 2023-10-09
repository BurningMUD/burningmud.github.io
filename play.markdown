---
layout: default
title: Play
---
# New Players Info
The first time you play, you may not need a client if you are just trying the game out. Just click play and create a game account and you can create a character to get started.

But as time goes, to play a MUD of any kind, you generally will want to find a client that can do some things like triggers, which are just means to automatically react to certain events. For example, a first trigger many people add is to eat food when the "You are hungry." message appears, allowing them to focus on more important tasks. You shouldn't feel like this is required to get started. It is more of an advanced feature. Many things can be accomplished using the in-game [Alias](help.markdown) system, allowing you to create shortcuts for commands you use a lot.

That said, triggers are not smart in the way a person is, and cannot anticiapte problems in the same way, and only do exactly what you told them to do. Sometimes, maybe during a fight if you become hungry, the best choice of action is usually not to eat food. So be careful with how you structure your reactions. If you string together a bunch of commands all at once, the commands are queued or stacked, and there is no way to cancel these actions, so if something unexpected happens during this time while waiting for your queue of commands to happen, you will be unable to react in time.
* * *

<div style="text-align: center">

# [Connect to BurningMUD](telnet://burningmud.com:4000)

</div>

# PC MUD Clients
While the MUD itself has no graphics so to speak, many popular Windows clients have their own GUI which lets your interact with a mouse to create triggers or other configs. This is preferred for most individuals who are not on Linux.

[Mudlet](https://www.mudlet.org/) - Newer client for Windows, Mac, and Linux. If you are unfamiliar with MUDs, this may be a good starting place.<br>
[ZMUD](https://www.zuggsoft.com/) - Legacy paid client for Windows.<br>
[CMUD](https://www.zuggsoft.com/) - Modern paid ZMUD replacement.<br>
[PuTTy](https://putty.org/) - Telnet / SSH Client for Windows.<br>
    - Connect directly to BurningMUD via Telnet protocol. PuTTy itself does not support triggers.<br>
    - Connect to a Linux SSH server where TinyFugue client is hosted.<br>
    - Generally used on Windows to connect to Linux server that has TinyFugue installed.

# PC Commandline Clients
These clients are run through the commandline, and do not require a mouse.

[TinyFugue (TF)](https://tinyfugue.sourceforge.net/) - A commandline client for Linux.<br>
[TinTin++](https://tintin.mudhalla.net/) - Legacy commandline client for Linux or Windows (WinTin++)<br>

# Mobile Clients
[JuiceSSH](https://juicessh.com/) - Android SSH or Telnet client.

* * *

# Telnet Protocol
Finally, if you don't want to install anything, you can always stop by using a Telnet client @ burningmud.com, port 4000.<br>
Just click the "Connect to BurningMUD" link at the top of the page to launch a telnet connection with your default client.
&nbsp;&nbsp;&nbsp;&nbsp;* Learn more about Telnet technicals and commandline usage at [Microsoft](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/telnet)<br>
&nbsp;&nbsp;&nbsp;&nbsp;* Learn how to enable built-in support for Telnet on Windows 10 at [Microsoft](https://social.technet.microsoft.com/wiki/contents/articles/38433.windows-10-enabling-telnet-client.aspx)


## Triggers
Find information and trigger files for your perferred client on the [Player Sites](/player_sites.markdown) page.