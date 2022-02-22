---

title: "Setup"
slug: "setup"
backgroundImage: "assets/images/bg_container.jpg"

---
# Setup

## Required File Downloads

Download and extract the following from MHFrontierSetup.zip:

- **ErupeServer.zip:** The [latest commit version](https://github.com/ErupeServer/Erupe/tree/f1bbc25b25fb08ad03b539b108a9e627b9c97a71) of the ErupeServer source repository prior to archiving. This comes with all available quest and scenario binaries prepackaged. NOTE: There are MANY quest binaries, so extracting this folder will take a WHILE (why not hunt a monster or two in the meantime?)
- **MHF-ZZ_Installed_Files.zip:** The game installation files. The majority of these files are sourced from [Archive.org](https://archive.org/search.php?query=%22monster%20hunter%20frontier%20Z%22) provided by fist.moe
- **installers (optional):** This has a Windows10 subfolder containing Go, PostgreSQL, Python3.8 installers that were verified to work on Windows 10 at the time of writing this guide. You can also obtain these from the official sites
- **run_client.bat:** A batch file for initiating the client. You MUST have Python3.8 installed (more on this below). You MUST run this shortcut as an administrator EVERYTIME you start the game: **Right-Click > Run as Administrator**
- **run_server.bat:** A batch file for initiating the server. You MUST have Go installed (more on this below)

## PostgreSQL Installation
Download and install the [latest version of PostgreSQL](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads) for your operating system (the Windows 10 version used in this guide is included inside the **installers > Windows10** folder)

Select the following required Components
  - PostgreSQL Server
  - pgAdmin 4
  - Command Line Tools

![installation components](assets/images/postgresql-components.jpg)

Create a password for the database user (this guide uses the default username `postgres` and password `admin`)

Select a port for the database server to listen to (this guide uses the port 5433)

Finish the installation


## Golang Installation
Download and install the [latest version of Golang](https://golang.org/dl/) for your operating system (the Windows 10 version used in this guide is included inside the **installers > Windows10** folder)

### Install `golang-migrate`.
Open Powershell (Windows Key + R > "Powershell" > Enter) and follow the steps below to successfully install [Scoop](https://scoop.sh/):
  - Run the following command to allow the execution of remote-signed code: `Set-ExecutionPolicyRemoteSigned -scope CurrentUser`
  - Run the following command to install scoop: `iwr -useb get.scoop.sh | iex`

Once Scoop has been installed, run the following command on a Powershell window to install [golang-migrate](https://github.com/golang-migrate/migrate/tree/master/cmd/migrate):
  - `scoop install migrate`


## Python 3.8 & Frida Installation
Download and install the [latest version of Python3.8](https://www.python.org/downloads/release/python-380/) for your operating system (the Windows 10 version used in this guide is included inside the **installers > Windows10** folder)

**IMPORTANT:** Make sure you enable the option to `Add Python 3.8 to PATH` This is REQUIRED in order to run the `py` command via run_client.bat

Once Python 3.8 has been installed, open up a new command prompt and run the following command: `pip install frida`

## Database Setup
Once PostgreSQL has been installed, open a new Command Prompt window (Windows key + R > "cmd" > Enter) and run the following command to connect to your local database server (`postgres` is the default user created during the installation):

```
psql -U postgres -h localhost -p 5433
```

Next, create the database `erupe` by entering the following command:

```
CREATE DATABASE erupe;
```

### Create the database tables
Open the ErupeServer folder via the Command Prompt (navigate to the folder via the File Explorer and replace the folder path at the top with `cmd` and hit Enter)

Enter the following command to run a database migration (replace the word "password" with the database password you created during installation):

`migrate -database postgres://postgres:password@localhost:5433/erupe?sslmode=disable -path migrations up`

This will create the database tables needed to run the game.


## Preparing config.json
If needed, edit the file `config.json` found inside `ErupeServer` You can use any text editor including Notepad to do this (Right-Click > Edit or Open With > Notepad)

![Edit Config JSON](assets/images/edit-config-json.jpg)

Modify the `username` and `password` fields and change it to the database credentials you selected during PostgreSQL installation.

![Edit Config JSON](assets/images/edit-config-json-2.jpg)

You can modify additional settings here and even replace all instances of 127.0.0.1 (localhost) with the External IPv4 Address of another hosted server (if playing with friends).

## Running the Server
You can now run/double-click the file `run_server.bat` where you unpacked your downloads.

This will open up a new Command Prompt window and automatically run the command `go run .` from within the `ErupeServer` folder which will start the server (you can also monitor database activity as you are playing the game).

If everything was configured correctly, you should not have to do anything else.

Leave this window open while you play the game.
Press `CTRL + C` to exit and shut down the server when you are done.

## Preparing the Client

### Edit your Windows HOSTS File

Open Notepad as administrator and navigate to your `HOSTS` file normally located under `C:/Windows/System32/drivers/etc/hosts` Add the following to the bottom and save:

```
127.0.0.1 mhfg.capcom.com.tw
127.0.0.1 mhf-n.capcom.com.tw
127.0.0.1 cog-members.mhf-z.jp
127.0.0.1 www.capcom-onlinegames.jp
127.0.0.1 srv-mhf.capcom-networks.jp
```

This will resolve your localhost IPv4 adddress to the several official CAPCOM domains, allowing the client to bypass CAPCOM's servers and connect to your local or external server address (Replace `127.0.0.1` if you are connecting to an external IPv4 address)

**IMPORTANT** Please be VERY careful not to modify anything else inside your System32 folder. This can damage your operating system.

### Changing your SYSTEM LOCALE

To run the client and play the game, you MUST set your System Locale to Japan:

Open Control Panel (View by: Category) > Clock And Region > Region > Administrative > Change System Locale > Current system locale > Japanese (Japan)

![changing locale to japan 1](assets/images/locale-to-japan.jpg)

![changing locale to japan 2](assets/images/locale-to-japan-2.jpg)

Reboot your PC for changes to take effect.

## Running the Client

Once the above has been configured, you must now right-click the file `run_client.bat` and run as administrator.

![run client as administrator](assets/images/run-client.jpg)

This .bat (batch file) opens a Command Prompt window and runs the Client-Patcher script `no_gg_jp.py` inside `MHF-ZZ_Installed_Files` which will bypass the GameGuard anti-cheat software originally included with the game.

To exit the client process, press `Ctrl + C`, type `Y` and hit Enter

If you get a Windows Security Alert that says "Windows Defender has blocked some features of this app" click "Allow Access"

![allow client through the Windows Defender Firewall](assets/images/run-client-2.jpg)

Wait several seconds as the `Erupe Simple Launcher` will now open in another window. Enter a Username or Password for your Monster Hunter Frontier profile. (Entering a new username and password will create a new profile)

![starting the client](assets/images/run-client-3.jpg)

The `Config` button opens the game configuration menu which allows you to change several game settings including display options. Make sure to check on **High Grade Edition** to enable HD texture and lighting settings. The second tab contains Full Screen and Windowed display resolution options. Once you are done, click OK and then OK on any prompts that appear.

Click `Submit` to proceed to the Character Select menu. Select your existing character or default profile when creating a new account and then click `Select` to start the game.

![select your character](assets/images/run-client-4.jpg)



