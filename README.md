# Lost in Time C Injection (based on plat_qol)
[Original Repository](hhttps://github.com/BluRosie/plat_qol)

C Injection Pokemon Platinum repository intended to be used in tandem with Following Platinum to create a number of Quality of Life changes that enhance the gameplay experience.

This repository is also structured to be extensible as a C injection template with the requisite infrastructure already set up for an aspiring hacker.

## Table of Contents

- [Features](#features)
- [Setup Instructions](#setup-instructions)
    - [Windows](#windows)
    - [Mac OSX](#mac-osx)
    - [Linux](#linux)
- [Build Instructions](#build-instructions)
- [Credits](#credits)

# Features:
<details>
<summary>- Unlimited TM's</summary>
<br>

![](screenshots/infinite_tms0.png)
</details>

<details>
<summary>- HM Usage based on possession</summary>
<br>

![](screenshots/usable_hm0.png) ![](screenshots/usable_hm1.png) 

![](screenshots/usable_hm3.png) ![](screenshots/usable_hm2.png)

![](screenshots/hms_usable.gif)

</details>

<details>
<summary>- Pressing B toggles autorun</summary>
<br>

![](screenshots/autorun.gif)

</details>

<details>
<summary>- Faster surfing speed</summary>
<br>

![](screenshots/surf_speed.gif)

</details>

<details>
<summary>- Press B to select RUN in wild battles</summary>
<br>

![](screenshots/run_from_battle.gif)

</details>

<details>
<summary>- Faster HP bar drain</summary>
<br>

![](screenshots/hp_drain.gif)

</details>


# Contributing
DM me on Discord (BluRose#0412)

## Setup Instructions

### Windows

Windows builds are based on WSL. If you do not have WSL set up (or do not know if you do), follow the instructions in [Setting up WSL](#setting-up-wsl) below.

If you already have a WSL environment set up, proceed to [Further Instructions](#further-instructions).

#### Setting up WSL

1. Enable Windows Subsystem for Linux.
    1. Open your command prompt as Administrator.
        1. In the search bar in the Start Menu, search for "cmd".
        2. Right-click on **Command Prompt**.
        3. Click **Run as Administrator**.
    2. Run the following command: `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all`.
    3. After the process completes, you will be prompted to restart your PC. Type "Y" and press **Enter** to restart.
    4. During the reboot process, enable virtualization in your BIOS.
        - The exact steps here will vary by system and the exact make/model of your PC's motherboard. You can find a general sketch of instructions [here](https://bce.berkeley.edu/enabling-virtualization-in-your-pc-bios.html).
2. Install Ubuntu.
    1. In the search bar in the Start Menu, search for "store" and open **Microsoft Store**.
    2. In the search bar of the window that opens, search for "Ubuntu".
    3. Click the blue **Get** button.
    4. Once installation is complete, launch Ubuntu from its page in the Microsoft Store to finish setup.
        - This will start a setup procedure that may take some time to complete.
    5. Once the setup procedure is complete, choose a username and password for the system.
3. Open WSL.
    1. Open the **Run** window by pressing the **Windows Key** and **R** at the same time.
    2. Type `wsl` into the window and press **Enter**.
4. Update WSL.
    1. In WSL, type `sudo apt update` and press **Enter**.
    2. After the update process completes, type `sudo apt upgrade` and press **Enter**.
        - This process may take a long time.
        - You may be prompted to confirm that WSL should restart automatically during package updates. Select **Yes** and press **Enter**.

#### Further Instructions

1. Download and install devkitPro-pacman.
    - In WSL, run the following commands:
        1. `wget https://apt.devkitpro.org/install-devkitpro-pacman`
        2. `chmod +x ./install-devkitpro-pacman`
        3. `sudo ./install-devkitpro-pacman`
2. Install necessary packages.
    - In WSL, run the following commands:
        1. `sudo apt-get install build-essential git libpng-dev gdebi-core python3 python3-pip cmake automake`
        2. `pip3 install ndspy`
        3. `dkp-pacman -S gba-dev`
3. Restart WSL, then run the following commands.
    1. `export DEVKITPRO=/opt/devkitpro`
    2. `echo "export DEVKITPRO=$DEVKITPRO" >> ~/.bashrc`
    3. `export DEVKITARM=$DEVKITPRO/devkitARM`
    4. `echo "export DEVKITARM=$DEVKITARM" >> ~/.bashrc`
    5. `cd Documents`
    6. `git clone https://github.com/lhearachel/plat-qol.git`
        - This will create a new directory `plat-qol`, which will be short-handed as "the project directory" from hereon.

### Mac OSX

TBD

### Linux

#### Debian-based (e.g. Debian, Ubuntu, Linux Mint)

1. Download and install devkitPro-pacman.
    - Follow the instructions listed [here](https://github.com/devkitPro/pacman/releases).
1. Install necessary packages.
    - In Terminal, run the following commands:
        1. `sudo apt install libpng-dev build-essential cmake python3-pip git automake`
        2. `pip3 install ndspy`
        3. `dkp-pacman -S gba-dev`

#### Arch-based (e.g. Arch Linux, Endeavour)

1. Import keys for devkitPro's repository.
    - Follow the instructions listed [here](https://devkitpro.org/wiki/devkitPro_pacman#Customising_Existing_Pacman_Install).
1. Install necessary packages.
    - In Terminal, run the following commands:
        1. `sudo pacman -S libpng base-devel cmake python-pip git automake gba-dev`
        2. `pip3 install ndspy`

#### Further Instructions (Platform Agnostic)

1. Restart Terminal, then run the following commands.
    1. `export DEVKITPRO=/opt/devkitpro`
    2. `echo "export DEVKITPRO=$DEVKITPRO" >> ~/.bashrc`
    3. `export DEVKITARM=$DEVKITPRO/devkitARM`
    4. `echo "export DEVKITARM=$DEVKITARM" >> ~/.bashrc`
    5. `cd Documents`
    6. `git clone https://github.com/lhearachel/plat-qol.git`
        - This will create a new directory `plat-qol`, which will be short-handed as "the project directory" from hereon.

## Build Instructions

1. Setup your ROM.
    - Your base ROM *must* be a verified dump of **Pokemon Platinum (US)**.
    - Perform any and all edits to scripts, maps, events, etc. to your ROM *before* you install this repository.
2. Place your ROM.
    - Place your finalized ROM into the project directory and rename it to `rom.nds`.
3. Navigate to the project directory in Terminal/WSL.
4. Download and build necessary tools.
    - Run `make build_tools -j$(nprocs)`. This process will download the source code for tools needed by the injection routine and compile them for you.
5. Make your ROM.
    - Run `make -j$(nprocs)`.
6. Test your ROM.
    - After the previous `make` process completes, a new file will appear in this folder named `build.nds`. This ROM will contain all injected routines and modifications from this project.


# Credits
* [**Skeli (FR template)**][CFRU]
* [**CodenamePU (NARC tool)**][G5T]
* [**Mikelan98, Nomura (ARM9 Expansion Subroutine )**][ARM9]
* Rafael Vuijk (Nintendo DS rom tool)
* [**pret/pokediamond**][pret]
* [**JimB16/PokePlat**][pokeplat]
* [**Bubble791 for base repo**]

[CFRU]: https://github.com/Skeli789/Complete-Fire-Red-Upgrade
[G5T]: https://github.com/CodenamePU/Gen5Tools
[ARM9]: https://pokehacking.com/tutorials/ramexpansion/
[pret]: https://github.com/pret/pokediamond
[pokeplat]: https://github.com/JimB16/PokePlat
