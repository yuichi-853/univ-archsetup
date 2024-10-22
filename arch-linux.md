# Arch Linux Setup Reference

# Table of Contents

<!-- TOC GFM -->

* [Arch Installation](#arch-installation)
    * [Storage](#storage)
    * [Host Name](#host-name)
* [Settings & Installation](#settings--installation)
    * [Connecting to Wi-fi](#connecting-to-wi-fi)
    * [Edit Settings](#edit-settings)
    * [Set a shortcut to open the terminal\"](#set-a-shortcut-to-open-the-terminal)
    * [Remap the \"annoying\" Capslock as the Control key](#remap-the-annoying-capslock-as-the-control-key)
    * [Install yay (Package manager)](#install-yay-package-manager)
    * [Install less, xclip, make, unzip & gcc](#install-less-xclip-make-unzip--gcc)
    * [Git configurations](#git-configurations)
    * [Install fonts](#install-fonts)
    * [Install Firefox](#install-firefox)
    * [Enable Fractional Screen](#enable-fractional-screen)
    * [Enable Japanese Input](#enable-japanese-input)
    * [Setup Bluetooth](#setup-bluetooth)
    * [Install Multipul Useful packages](#install-multipul-useful-packages)
    * [Setup NeoVim (The best text editor ever)](#setup-neovim-the-best-text-editor-ever)
    * [Setup Kitty](#setup-kitty)
    * [Setup tmux](#setup-tmux)
    * [Enable Starship prompt](#enable-starship-prompt)
    * [Setup Gnu Stow](#setup-gnu-stow)

<!-- TOC -->

# Arch Installation
Follow [this instruction
video](https://www.youtube.com/watch?v=FxeriGuJKTM).

## Storage
ext4

## Host Name
Don\'t set it to \"Arch Linux\"! It\'s PC\'s identication name, so it
should be unique like \"UserName-ThinkPad-E14-G6\".

# Settings & Installation
## Connecting to Wi-fi
When the installation is complete, connect it to Wi-fi.

## Edit Settings
-   Settings \> Keyboard \> Alternate Characters Key \> Change to Left
    Alt
-   Settings \> Navigation \> Move window one workspace to the
    left/right \> Shift+Super+Left/Right
-   Settings \> Navigation \> Switch to workspace on the left/right \>
    Ctrl+Super+Left/Right
-   Settings \> Navigation \> Switch windows \> Alt+Tab
-   Settings \> Multitasking \> General \> Unable Hot Corner
-   Settings \> Multitasking \> Multi-Monitor \> \"Enable Workspaces on
    all displays\"

## Set a shortcut to open the terminal\"
Keyboard \> View and Customize Shortcuts

-   Name: terminal
-   Command: kgx
-   Shortcut: Ctrl+Alt+T

## Remap the \"annoying\" Capslock as the Control key
Tweaks \> Keyboard \> Aditional Layout Options \> Ctrl position \> Caps
Lock as Ctrl

## Install yay (Package manager)
Install the required base-devel and git.
``` bash
sudo pacman -S base-devel git
```

Clone the yay repo. Once done, switch to the cloned directory.
``` bash
git clone https://aur.archlinux.org/yay.git
cd yay
```

Build the package from the following command.
``` bash
makepkg -si
```

Once the process finishes, verify that the yay has been installed
successfully.
``` bash
yay --version
```

## Install less, xclip, make, unzip & gcc
``` bash
sudo pacman -S less xclip make unzip gcc
```

## Git configurations
``` bash
git config --global user.name "John Doe"
git config --global user.email "johndoe@example.com"
git config --global init.defaultBranch main
git config --global url."git@github.com:".insteadOf "https://github.com/"
git config --list
```

Increase Git\'s http buffer size to 1gb from the following command.
``` bash
git config --global http.postBuffer 1048576000
```

## Install fonts
``` bash
sudo pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
```

## Install Firefox
``` bash
sudo pacman -S firefox
```

## Enable Fractional Screen
``` bash
gsettings set org.gnome.mutter experimental-features "['scale-monitor-framebuffer']"
```

## Enable Japanese Input
### 1. Edit Locale
Locale is in /etc/locale.gen file.
``` bash
cd ../../etc
sudo vim locale.gen
```

Then, uncomment the \`ja~JP~, UTF-8\` part.
Type \`:wq\` in nomal mode to quit.
Afterthat, regenerate locale.
``` bash
locale-gen
```

### 2. Install Fcitx5 (IMF: Imput Method Framework)
Install fcitx5-im & GUI config tool.
``` bash
sudo pacman -S fcitx5-im fcitx5-configtool
```
At the \"Repository extra\" prompt, just hit \`Enter\` (select all).

### 3. Set some environmental variables.
``` bash
sudo vim environment
```
Then add these three environmental variables.
``` eshnv
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

### 4. Install Mozc (IME: Input Method Editor)
``` bash
sudo pacman -S fcitx5-mozc
```

### 5. Set Mozc as an input method
Launch the setup GUI application.
``` bash
cd ~
fcitx5-config tool
```
Search for the input method \`Mozc\`, select it, and then click the
\`Apply\` button.

### 6. Apply the changes
To apply the changes, log out of your computer and log back in. This
will ensure that all the new settings are correctly loaded.

## Setup Bluetooth
``` bash
sudo pacman -S bluez bluez-utils
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

## Install Multipul Useful packages
### With yay
``` bash
yay -S brave-bin strawberry google-chrome
```
At the \"Packages to cleanBuild\" prompt, select \`All\`, and at the
\"Diffs to show\" prompt, select \`None\`.

### With pacman
``` bash
sudo pacman -Syy
sudo pacman -S vlc kid3 nodejs npm tree inkscape gmp
```
At the \"qt6-multimedia-backend\" prompt, select \`1)
qt6-multimedia-ffmpeg\`.

### With npm
``` bash
sudo npm i -g vscode-langservers-extracted
sudo npm i -g ls_emmet
```

## Setup NeoVim (The best text editor ever)
### Install nerd-font
You can download the .zip file from [here](https://www.nerdfonts.com/)
(for example, the \'JetBrainsMono\' font). After downloading, you can
extract it.
1.  Unzip the file

    ``` bash
    unzip ~/Downloads/jetbrainsmono.zip -d ~/Downloads/jetbrainsmono
    ```

2.  Create the font directory
    ``` bash
    mkdir -p ~/local/share/fonts
    ```

3.  Move the extracted font folder to the correct location
    ``` bash
    mv ~/Downloads/jetbrainsmono ~/.local/share/fonts/
    ```

4.  Update the font cache
    ``` bash
    sudo fc-cache -fv
    ```

### Install NeoVim
``` bash
sudo pacman -S neovim
```

## Setup Kitty
### Install Kitty
``` bash
sudo pacman -S kitty
```

## Setup tmux
### Install tmux
``` bash
sudo pacman -S tmux
yay -S tmux-bash-completion-git
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### Configure tmux

## Enable Starship prompt
### Install & initialize Starship
``` bash
sudo pacman -S starship
```
And add these line below on ~/.bashrc.
``` bash
eval "$(starship init bash)"
```

## Setup Gnu Stow
### Install Stow
``` bash
sudo pacman -S stow
```

### Setup PC using Gnu Stow

``` bash
git clone git@github.com:yuichi-853/dotfiles.git
cd dotfiles
mv ~/dotfiles/.config/nvim ~/.config
mv ~/dotfiles/.config/kitty ~/.config
stow --adopt .
cp -r ~/.config/nvim ~/dotfiles/.config
cp -r ~/.config/kitty ~/dotfiles/.config/
stow --adopt .
```


Boom! It\'s done! Welcome to Arch Linux!!!
