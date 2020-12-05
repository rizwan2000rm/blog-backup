## Linux Web Development Enviorment in Windows 10


Photo by Kevin Ku on Unsplash

This article goes over how to create a Linux development environment (for web development) in Windows 10

**Pre-requisites for WSL2 requirements**

* Running Windows 10, updated to **version 1903 or higher**, Build 18362 or higher for x64 systems.

* Running Windows 10, updated to version 2004 or higher, **build 19041**, for ARM64 systems.

* Check your Windows version by selecting the **Windows logo key + R**, type **winver**, press **ENTER**. (Or enter the ver command in Windows Command Prompt). Please update to the latest Windows version if your version is lower.

**Install the Windows Subsystem for Linux**

Open PowerShell as Administrator and run:

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

```


Restart your system and open powershell as administrator again

```
wsl - set-default-version 2
```


**Install your Linux distribution of choice**

Open the Microsoft Store and select your favorite Linux distribution from a variety of distributions like Ubuntu, Debian, Kali Linux, and many more (I prefer Debian, but any Debian based distribution will work just fine).

* From the distribution’s page, select Get.

* Find the distribution in the Start Menu and open it.

The first time you launch a newly installed Linux distribution, a console window will open, and you’ll have to set up a username and password.

If you faced any errors during the installation, follow instructions on [this link](https://docs.microsoft.com/en-us/windows/wsl/install-win10#troubleshooting-installation), and check for the specific error you are facing.

**Installing tools for web development**

Now type this commands in the Linux Terminal you opened

* **Installing packages**

```
sudo apt update
sudo apt -y upgrade
sudo apt install -y git curl wget zsh python3.8 unzip
```


* **Terminal utilities **I like to use like **exa **(modern replacement for ls), **syntax highlight**, **auto-suggestions**, and **auto-jump **(helps you jump into nested directories with one command rather than using **cd /directory1/…./directory-you-want-to-cd-into**, now you can just use** j directory-you-want-to-cd-into,** *provided you have cd into that directory before*

The first line below will prompt you to change the default shell to zsh after execution, type y and press Enter to change the default shell

```
sh -c "$(curl -fsSL [https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh](https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh))"

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone git://github.com/wting/autojump.git
python3 ~/autojump/install.py

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

cd
curl https://sh.rustup.rs -sSf | sh
wget -c https://github.com/ogham/exa/releases/download/v0.9.0/exa-linux-x86_64-0.9.0.zip
unzip exa-linux-x86_64-0.9.0.zip
sudo mv exa-linux-x86_64 /usr/local/bin/exa
```


* **Setting Up VS Code with WSL**

All you need to do is, launch VS Code. It will prompt you to install Remote WSL Extension, or you can manually install it.

* **Now you have to change .zshrc file to finish setting up Terminal Utilities**

```
code ~/.zshrc
```


The above command will open a file in VS Code, replace content of that file with the one below and save. ***Make sure to replace USERNAME with your Linux Username while replacing.***

```shell
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="/home/USERNAME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="powerlevel10k/powerlevel10k"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment the following line to disable bi-weekly auto-update checks.
# DISABLE_AUTO_UPDATE="true"

# Uncomment the following line to automatically update without prompting.
# DISABLE_UPDATE_PROMPT="true"

# Uncomment the following line to change how often to auto-update (in days).
# export UPDATE_ZSH_DAYS=13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
zsh-autosuggestions
zsh-syntax-highlighting
git
)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
alias mv="mv -i"
alias rm="rm -i"
alias gs="git status"
alias ls="exa -la -G --colour=auto --git"
alias lt="exa -T -L=2 -l --colour=auto"

# Autojump
[[ -s /home/USERNAME/.autojump/etc/profile.d/autojump.sh ]] && 
source /home/USERNAME/.autojump/etc/profile.d/autojump.sh

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

# nvm
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

Now load these configs on the terminal by

```
source ~/.zshrc
```


Now you will be prompted to customize Linux Prompt Theme, **it might not look so the way it should because we don’t have powerline fonts but we will fix it in Windows Terminal as I never use the default Linux Terminal anyway. Just choose the options you like for now, it will look smooth with icons and everything in Windows Terminal. **You can always re-run the configuration by command **p10k configure.**

I also like to use Windows Terminal from Microsoft so I can jump between many different shells quickly

* Open the Microsoft Store, search for Windows Terminal and select Get.

You can customize Windows Terminal as per your liking, for reference use this [**video](https://www.youtube.com/watch?v=oHhiMf_6exY) **and the official [**Microsoft Docs](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/profile-settings).**

Now set the same** Cascadia Code PL **Font for the Linux Distribution or set the font as a global config. I also like to have a background image on Windows Terminal, you can use my config too. **Again change USERNAME before copy pasting**

```json
// To view the default settings, hold "alt" while clicking on the "Settings" button.
// For documentation on these settings, see: https://aka.ms/terminal-documentation

{
  "$schema": "https://aka.ms/terminal-profiles-schema",

  "defaultProfile": "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",

  "profiles": {
    "defaults": {
      // Put settings here that you want to apply to all profiles
      "fontFace": "Cascadia Code PL",
      "fontSize": 16,
      "useAcrylic": true,
      "acrylicOpacity": 0.7,
      "cursorShape": "vintage",
      "colorScheme": "SpaceGray",
      "backgroundImage": "C:\\Users\\USERNAME\\Pictures\\terminal.jpg",
      "backgroundImageStretchMode": "fill",
      "backgroundImageOpacity": 0.1,
      "cursorColor": "#00FF00"
    },
    "list": [
      {
        "guid": "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
        "hidden": false,
        "name": "Debian",
        "startingDirectory": "//wsl$/Debian//home//USERNAME",
        "fontFace": "MesloLGS NF",
        "tabTitle": "Debian",
        "suppressApplicationTitle": true,
        "source": "Windows.Terminal.Wsl"
      },
      {
        "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
        "startingDirectory": "//wsl$/Ubuntu-20.04//home//USERNAME",
        "hidden": false,
        "fontFace": "MesloLGS NF",
        "tabTitle": "Ubuntu",
        "suppressApplicationTitle": true,
        "name": "Ubuntu",
        "source": "Windows.Terminal.Wsl"
      },
      {
        // Make changes here to the powershell.exe profile
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "name": "Windows PowerShell",
        "commandline": "powershell.exe",
        "hidden": false
      },
      {
        // Make changes here to the cmd.exe profile
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "name": "cmd",
        "commandline": "cmd.exe",
        "hidden": false
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": true,
        "name": "Azure Cloud Shell",
        "source": "Windows.Terminal.Azure"
      }
    ]
  },

  // Add custom color schemes to this array
  "schemes": [
    {
      "name": "synthwave",
      "black": "#000000",
      "red": "#f6188f",
      "green": "#1ebb2b",
      "yellow": "#fdf834",
      "blue": "#2186ec",
      "purple": "#f85a21",
      "cyan": "#12c3e2",
      "white": "#ffffff",
      "brightBlack": "#000000",
      "brightRed": "#f841a0",
      "brightGreen": "#25c141",
      "brightYellow": "#fdf454",
      "brightBlue": "#2f9ded",
      "brightPurple": "#f97137",
      "brightCyan": "#19cde6",
      "brightWhite": "#ffffff",
      "background": "#000000",
      "foreground": "#dad9c7"
    },
    {
      "name": "SpaceGray Eighties Dull",
      "black": "#15171c",
      "red": "#b24a56",
      "green": "#92b477",
      "yellow": "#c6735a",
      "blue": "#7c8fa5",
      "purple": "#a5789e",
      "cyan": "#80cdcb",
      "white": "#b3b8c3",
      "brightBlack": "#555555",
      "brightRed": "#ec5f67",
      "brightGreen": "#89e986",
      "brightYellow": "#fec254",
      "brightBlue": "#5486c0",
      "brightPurple": "#bf83c1",
      "brightCyan": "#58c2c1",
      "brightWhite": "#ffffff",
      "background": "#222222",
      "foreground": "#c9c6bc"
    },
    {
      "name": "SpaceGray Eighties",
      "black": "#15171c",
      "red": "#ec5f67",
      "green": "#81a764",
      "yellow": "#fec254",
      "blue": "#5486c0",
      "purple": "#bf83c1",
      "cyan": "#57c2c1",
      "white": "#efece7",
      "brightBlack": "#555555",
      "brightRed": "#ff6973",
      "brightGreen": "#93d493",
      "brightYellow": "#ffd256",
      "brightBlue": "#4d84d1",
      "brightPurple": "#ff55ff",
      "brightCyan": "#83e9e4",
      "brightWhite": "#ffffff",
      "background": "#222222",
      "foreground": "#bdbaae"
    },
    {
      "name": "SpaceGray",
      "black": "#000000",
      "red": "#b04b57",
      "green": "#87b379",
      "yellow": "#e5c179",
      "blue": "#7d8fa4",
      "purple": "#a47996",
      "cyan": "#85a7a5",
      "white": "#b3b8c3",
      "brightBlack": "#000000",
      "brightRed": "#b04b57",
      "brightGreen": "#87b379",
      "brightYellow": "#e5c179",
      "brightBlue": "#7d8fa4",
      "brightPurple": "#a47996",
      "brightCyan": "#85a7a5",
      "brightWhite": "#ffffff",
      "background": "#20242d",
      "foreground": "#b3b8c3"
    },
    {
      "name": "Tomorrow Night Eighties",
      "black": "#000000",
      "red": "#f2777a",
      "green": "#99cc99",
      "yellow": "#ffcc66",
      "blue": "#6699cc",
      "purple": "#cc99cc",
      "cyan": "#66cccc",
      "white": "#ffffff",
      "brightBlack": "#000000",
      "brightRed": "#f2777a",
      "brightGreen": "#99cc99",
      "brightYellow": "#ffcc66",
      "brightBlue": "#6699cc",
      "brightPurple": "#cc99cc",
      "brightCyan": "#66cccc",
      "brightWhite": "#ffffff",
      "background": "#2d2d2d",
      "foreground": "#cccccc"
    },
    {
      "name": "Tomorrow Night Blue",
      "black": "#000000",
      "red": "#ff9da4",
      "green": "#d1f1a9",
      "yellow": "#ffeead",
      "blue": "#bbdaff",
      "purple": "#ebbbff",
      "cyan": "#99ffff",
      "white": "#ffffff",
      "brightBlack": "#000000",
      "brightRed": "#ff9da4",
      "brightGreen": "#d1f1a9",
      "brightYellow": "#ffeead",
      "brightBlue": "#bbdaff",
      "brightPurple": "#ebbbff",
      "brightCyan": "#99ffff",
      "brightWhite": "#ffffff",
      "background": "#002451",
      "foreground": "#ffffff"
    },
    {
      "name": "cyberpunk",
      "black": "#000000",
      "red": "#ff7092",
      "green": "#00fbac",
      "yellow": "#fffa6a",
      "blue": "#00bfff",
      "purple": "#df95ff",
      "cyan": "#86cbfe",
      "white": "#ffffff",
      "brightBlack": "#000000",
      "brightRed": "#ff8aa4",
      "brightGreen": "#21f6bc",
      "brightYellow": "#fff787",
      "brightBlue": "#1bccfd",
      "brightPurple": "#e6aefe",
      "brightCyan": "#99d6fc",
      "brightWhite": "#ffffff",
      "background": "#332a57",
      "foreground": "#e5e5e5"
    }
  ],

  // Add any keybinding overrides to this array.
  // To unbind a default keybinding, set the command to "unbound"
  "keybindings": []
}

```

Now **run p10k configure in Linux Terminal again if you want**, and enjoy your beautiful terminal and linux setup in Windows itself.

Happy Hacking !!!