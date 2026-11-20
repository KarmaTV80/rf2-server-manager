# RF2 Server Manager

**English** · [Italiano](README.it.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [Português](README.pt.md)

**Download:** [latest version](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

**Support the project:** [donate with PayPal](https://www.paypal.com/donate/?business=3T7ZTAXBQY3EN&no_recurring=0&item_name=Sostieni+Karma+TV%3A+progetti+e+canali+YouTube%2C+Instagram%2C+TikTok.+Support+my+projects+and+channels.+Grazie%21+Thanks%21&currency_code=EUR) – the app is free, every donation helps keep it updated.

---

A Windows tool that sets up and runs an RF2 dedicated server.
It is not an official product and is not affiliated with Studio 397 or Motorsport Games.

At first start the app detects the Windows language: Italian, English, Spanish, French, German or Portuguese. Any other language falls back to English. The flag button at the top right changes it, and the app remembers your choice.

## Requirements

- Windows 10 or 11, 64-bit. .NET is already included in the exe.
- Disk space for the server and the content.
- Microsoft Edge WebView2 Runtime, only for the browser in the Workshop tab. Without it, you can paste the Workshop ID by hand.

The dedicated server and SteamCMD are not included: the app can download them from Valve and Steam with the setup wizard.

## First start

1. Run `RF2ServerManager.exe`. No installation is needed.
2. If Windows shows "Windows protected your PC", choose **More info** and then **Run anyway**. It appears because the exe has no digital signature.
3. In the setup wizard choose the SteamCMD and server folders, or let the app download them.
4. Start the server once: it creates its configuration files. If Windows asks for firewall permission, choose **Allow**.

## Updates

At start the app checks on GitHub whether a new version is available. If there is one, an **Update now** box appears at the bottom of the left menu. The app downloads it, checks its SHA-256 fingerprint and reopens by itself; a server that is on stays on. Below the version number, **Check for updates** checks again by hand. If the app's folder cannot be written to (for example inside Program Files), download the new version from the [releases page](https://github.com/KarmaTV80/rf2-server-manager/releases).

## Content you already have in the game

You don't need to download it again or copy it by hand. The app finds the game folder by itself, and you can also choose it in step 1. Setup. In step 3. Content press **Add from game**, select cars and tracks and press **Copy to server**. The game is only read.

In **Library** each item shows its state: *Ready*, *To install* or *Package missing*, when friends cannot download it. The button on the row does the right thing: it installs, copies the package from the game, or opens the Workshop searching for that item. The event's cars and tracks are chosen in step 4. Event, with **Create a new event**.

Content installed in the game without an `.rfcmp` package (for example bought from a website) appears at the bottom of the lists: its installation is copied to the server, and only drivers who already have it, in the same version, can join.

Official DLC you bought works on the server: the app copies by itself the unlock file the game prepares (`ServerUnlock.bin`). Content updates are applied by themselves too.

## Playing with other people

On the router, forward to the PC's IP:

| Port | Protocol | Use |
|---|---|---|
| 54297 | TCP and UDP | Simulation |
| 64297 | TCP | File downloads by clients |
| 64298 and 64299 | UDP | Steam: without them the server doesn't appear in the game's list |

**Never open ports 5397 and 5398**: they control the server and the game. Always set a join password and an admin password that differ from each other. The **Check network and ports** button in step 10. Server helps you check.

## Anti-cheat

In step 9. Chat and ping the app can report drivers with impossible laps or speeds and jumps from one point of the track to another, comparing each driver with the others in the same class. It disconnects nobody: it warns you and writes everything to the suspects log (`sospetti.log`), then whoever runs the server decides. The server cannot see inside the drivers' PCs, so it finds the effects of cheats, not the programs.

## Where the data is

- Settings and log: `%AppData%\RF2ServerManager`
- Passwords: only in the server's configuration files, which store them in plain text. They don't go into the profiles.

## Reporting a problem

Use **Report** at the top right of the app, or **Info → Report a problem** (from version 1.0.6). The app shows the log with Windows user name, driver names, Steam IDs, IP addresses and chat messages already removed, saves it to a text file and opens the [report form](https://github.com/KarmaTV80/rf2-server-manager/issues/new?template=segnalazione.yml) on GitHub: describe what happened and attach the file. Reports are public and need a free GitHub account. The **Open log folder** button is in step 1. Setup.

## Known limits

- Building mods and installing packages drive MAS2 and ModMgr in the background, with their windows hidden: progress shows in the app's log. With "Start the session right away" the server window also starts minimized: reopen it from the Windows taskbar. An update of those tools may require adapting the app.
- Paid content and packages copied from the Workshop may fail to install: the app shows the error and cleans up the files.
- Practice 2 has no start time and duration of its own in the server configuration.

## Terms of use

Free, also for championships and leagues. Modifying, decompiling, reselling or distributing it from other sites is not allowed: share only the official link. Full text in `LICENSE.txt` and in the app's **About** window.

Third-party components: FlaUI and Newtonsoft.Json (MIT license), Microsoft WebView2 SDK (Microsoft license), .NET (MIT license), Saira Extra Condensed and Barlow fonts (SIL Open Font License, texts in `Licenze\`).
