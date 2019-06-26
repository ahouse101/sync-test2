# Mac for Windows Developers
##### Tips, tricks, and tools for moving to macOS as a daily development environment.
-------------------------------------------------------------------------------
So you've been hired at a company that uses Mac exclusively as its development platform, but your experience is with Windows. Luckily, the switch doesn't have to be difficult. In this document, I go over major differences in UX, keyboard shortcuts, development style, day-to-day use, and helpful tools, and I provide my references both inline and at the end.

[Dan Rodney's Mac](https://www.danrodney.com/mac/) site is another great quick reference for casual users, and if you're truly new to Mac it's a nice "Cheat Sheet."

### Keyboard Shortcuts
- Keyboard shortcuts often use CMD instead of CTRL on Windows.
- Most Mac apps and documentation (as well as the rest of this document) refers to the modifier keys with their symbols:
	- `⌘` Command
	- `⌥` Option
	- `⇪` Caps Lock
	- `⇧` Shift
	- `⌃` Control
- Reference: [Apple Support - Mac keyboard shortcuts](https://support.apple.com/en-us/HT201236)

### Core UX Differences
- Gestures are core to the interface. It's worth learning all of them, directly from [Apple Support](https://support.apple.com/en-us/HT204895). Notably, you can get the same effect as four finger swipe up or down with the keyboard shortcuts `⌘Up` and `⌘Down` (arrow keys).
- Many basic differences are documented by Apple at "[Mac tips for Windows switchers](https://support.apple.com/en-us/HT204216)". That page covers UI differences more exhaustively than this document.
- `Alt+Tab` in Windows moves between windows on your desktop in MRU order. In macOS, there is no direct equivalent - `⌘Tab` will move you through your open apps (if an app has more than one window, it will focus the top level one and ignore the others), while ``⌘` `` (that's `CMD + backtick`) will cycle you through the current application's windows.
- In Windows, applications usually close when you close the last window. In macOS, most apps will continue to run when all windows are closed. In order to fully quit an app, you can use the system shortcut `⌘Q`. Some apps will quit fully when you close their windows (Eclipse, for example, or system utilities like Calculator or System Preferences).
- Several top-level window interactions work slightly differently in macOS. Minimize (`⌘M`) is the yellow button, which sticks your window (NOT your app, only the current window) on the right side of the Dock, still running but not reachable by ``⌘` ``. Hide (`⌘H`) has no button - it hides the current app (every window) but doesn't terminate anything, so if you switch to the app with the keyboard or Dock, it will come back instantly (this can be useful for apps that unload their configuration when closed). Close (`⌘W`) is the same as clicking on the red "traffic light" button on a window (which, by the way, will contain a dot if there's unsaved data in that app or an X if not).
- Fullscreen/zoom in macOS is totally different than Maximize in Windows. Most apps will use the green button to go into the new macOS full screen mode, which hides borders (if you hold the button instead, you can actually put two apps side-by-side in fullscreen). However, if you hold Option while clicking the Fullscreen button (or double click the titlebar of the window), you get the old Zoom behavior, which expands the window to fit all the content (not necessarily filling the screen). To get back some Windows behavior, I use Spectacle, discussed below.
- Many files are hidden from users by default. Like Linux, any file starting with a period is hidden, as well as many macOS system folders (like `Library`) and underlying UNIX paths (like `/usr/bin` or `/etc`, for instance). You can toggle showing these hidden paths at any time with the shortcut `⌘⇧.`, which I remember because it uses the "dot" key to show "dot files".
- Using the system `Apple Menu -> Sleep` option will pause running processes, so if you want to leave long-running processes open but turn off your display (for instance, if you walk away) you can use the terminal command `pmset displaysleepnow`, which will require your password/TouchID on wakeup just like sleep.

### Misc Tips
- The Dock works pretty differently than the Windows taskbar. I personally find it easiest to just change paradigm from Windows and autohide it (since it only shows up on one monitor anyway and tends to get in my way). Annoyingly, though, there's a pretty long show/hide delay when it's hidden, which [you can disable by following this guide](http://osxdaily.com/2012/03/27/remove-auto-hide-dock-delay-mac-os-x/).

### Is Mac UNIX?
As of newer versions, macOS is a certified POSIX system, so you get `bash` and most of the things you would expect on a typical Linux distro. That said, there's no `apt-get` or support for Debian-style repositories - instead, most developers use [Homebrew](https://brew.sh/), which you'll have installed when you set up your dev environment. [MacPorts](https://www.macports.org/) is an alternative package manager that you likely won't need, but has more Linux packages than Homebrew right now (although many are out of date).

From a technical side, High Sierra uses the newer APFS file system, which has similar features as NTFS in Windows, but all older version will use HFS+, which was designed for the older, pre-NeXTSTEP Mac OS 9. This system was not POSIX compliant, and it didn't support UNIX permissions, thus sometimes you had to reset your file permissions when the compatibility layer corrupted them. HFS+ also has the wrong endianness, so bytes have to be reversed as they're read from disk. Luckily, you shouldn't have worry about HFS+ on newer Macs (anything High Sierra and later).

### Recommended Utilities
By design, macOS only exposes minimal configuration to the user. This can sometimes be annoying, resulting in behavior that can only be fixed with external tools.
- [Spectacle](https://www.spectacleapp.com/) allows you to quickly lay out windows via keyboard shortcuts. There are other tools with more features or more UI, but most aren't free, and Spectacle works quite well. It lets you quickly split the screen up into thirds or halves, in either direction, or quickly expand a window to fill the screen without covering the Dock or titlebar (like Maximize in Windows). I think having a proper window snapping tool complements the native macOS Split Screen and Fullscreen views instead of replacing them.
- [Scroll Reverser](https://pilotmoon.com/scrollreverser/) is an extremely basic utility that lets you choose scroll direction for your mouse and touchpad independently. Annoyingly, there are two separate settings for this in System Preferences, but they're linked, and the only way to have normal scrolling on your mouse but proper reverse scrolling on your touchpad is to use this app.
- [Caffeine](http://lightheadsw.com/caffeine/) keeps your Mac awake, which is otherwise impossible to do, even if you disable sleep and screen saver. I also personally delete the ServiceNow screensaver and background, since they have an annoying tendency to keep popping back up if you change them.
- [iTerm2](https://www.iterm2.com/) The macOS Terminal.app is definitely more capable than the built-in Command Prompt in Windows, but I prefer iTerm2. It integrates very extensively into the macOS environment, even integrating touchpad gestures.
- Some at ServiceNow use SourceTree, but I don't really like it. Instead, I use [GitKraken](https://www.gitkraken.com/), which is particularly good at visualizing the tree and showing diff/blame details.
- If you used KeePass on Windows, it's no use trying to run that client on Mac. However, the native [MacPass](https://github.com/MacPass/MacPass) or the Electron-based [KeeWeb](https://keeweb.info/) are good alternatives.
- [Atom](https://atom.io/) (which I use), [Sublime Text](https://www.sublimetext.com/), and [VS Code](https://code.visualstudio.com/) all work equally well on Mac (for the most part), and there's also the macOS-only [TextMate](https://macromates.com/), which I've never used but some Mac users swear by.

### All References
- [Apple Support - Mac tips for Windows switchers](https://support.apple.com/en-us/HT204216)
- [Apple Support - Mac keyboard shortcuts](https://support.apple.com/en-us/HT201236)
- [Apple Support - Use Multi-Touch gestures on your Mac](https://support.apple.com/en-us/HT204895)
