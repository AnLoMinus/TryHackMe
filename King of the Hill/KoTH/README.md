>בס״ד
<div align="center">

![image](https://user-images.githubusercontent.com/51442719/172729066-1293d382-4a31-4f03-8c23-ab0ea5f611a0.png)

# `Anlominus` 🤴 [King of the Hill](https://tryhackme.com/games/koth)

---

```shell
wget https://raw.githubusercontent.com/Anlominus/TryHackMe/main/King%20of%20the%20Hill/KoTH/KoTH & sudo sh KoTH
```

</div>

---

# 📜 Menu ~ To Do
- 📜 Menu
  - [ ] [1] ~ Start THM ~> TryHackMe VPN
  - [ ] [2] ~ Start KoTH ~> King of The Hill

---

```shell
#!/bin/sh
#!/bin/bash
#!/usr/bin/bash
#!/usr/bin/env bash
#!/data/data/com.termux/files/usr/bin/bash
###############################################
# Name : Anlominus ~ KoTH
# Last UPDATE : 2022 Jun 10
# Create Date : 2022 Jun 10
# Description: TryHackMe - Simple helper script for VPN, VM's, etc
# Skils: Best Copywriter IN the COSMOS!
# BIG THANX TO ALL COMUNITY THAT SHARE ALL THAT FREE GREAT SCRIPTS
# CREDIT: To All World Creators free Scripts & Tools
# Location: Made With LOVE IN ISRAEL !
# Source: [ https://github.com/Anlominus/TryHackMe/tree/main/King%20of%20the%20Hill/KoTH ]
# Aouther: f11snipe +~> Anlominus ~> RhytMix ~> KoTH
###############################################
clear

# COLORS! :)
red='\033[0;31m'
cyan='\033[0;36m'
blue='\033[0;34m'
yellow='\033[0;33m'
nocolor='\033[0m'

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
  echo "\n\t\t $red Location exists $yellow >[ $vpn_dir ]< "

else
  echo "\n\t\t $yellow Creating .vpn Folder In $HOME/ Directory\n" & `mkdir $HOME/.vpn`

fi

# Define variable for our search string (find this running process)
vpn_file="$vpn_dir/$username.ovpn"

# Regex pattern to validate IP format (#.#.#.#)
valid_ip="([0-9]{1,3}\.){3}"
valid_thm=".*\.thm$"

# Session logfile
session_log=$vpn_dir/session.log

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
  if [[ "$vpn_running" != "0" ]]; then
    warn "🤨 THM VPN is not running!"
    warn "Searching for process: '$vpn_file' (using ps aux | grep ...)"

    if confirmYes "Connect to VPN now? (requires sudo)"; then
      sudo echo "init" > $session_log
      sudo -b openvpn $vpn_file > $session_log 2>&1 &

      log "Done! 😁"
    fi
  else
    log "THM VPN Connection Confirmed 👍"
  fi
}

# Check if openvpn connection is running
ps aux | grep "$vpn_file" | grep -v grep > /dev/null
vpn_running=$?

if [[ "$arg1" == "kill" ]]; then
  if [[ "$vpn_running" == "0" ]]; then
    log "Found running openvpn process(es):"
    ps aux | grep "$vpn_file" | grep -v grep

    if confirmYes "Kill all process(es)?"; then
      sudo pkill -f "$vpn_file"

      if [[ "$?" == "0" ]]; then
        log "They're ... all ... dead 🤥"
        exit 0
      else
        error "EPIC FAIL"
      fi
    else
      warn "Aborting 'kill' command"
    fi
  fi
elif [[ "$arg1" == "log" ]]; then
  cat $session_log
  log "This sesion log file is located: $session_log"
elif [[ $arg1 =~ $valid_ip ]]; then
  connectVpn
  if confirmYes "Update profile with VMIP=$arg1  "; then
    res=$(cat $profile_file | sed -e "s/VMIP=\(.*\)\( \#.*\)/VMIP=$arg1/g" | grep VMIP)
    log "Editing $profile_file: $res"
    sed -i'.bak' -e "s/VMIP=\(.*\)/VMIP=$arg1/g" $profile_file
    log "Run: 'source $profile_file' (to reload this session, new terminals will have \$VMIP set automatically)"
  else
    warn "Aborting new vm session"
  fi

  if [[ $arg2 =~ $valid_thm ]]; then
    warn "ADD AS HOST [/etc/hosts]: $arg1    $arg2"
  fi
else
  connectVpn
fi
```
