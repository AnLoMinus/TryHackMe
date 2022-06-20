# koth-protect-king
A script to protect your king in KoTH

# A script to protect your king

## Mode of use 

```
git clone https://github.com/MatheuZSecurity/koth-protect-king 
```

```
cd koth-protect-king && python3 -m http.server 80
```

## In KoTH Machine

```
wget http://youripvpn/king.sh && chmod +x king.sh && ./king.sh
```

#### then you just put your nick and the script already does all the work

![king](https://user-images.githubusercontent.com/88067225/168189766-61b494d2-12e5-4393-beb9-9978a88615f2.png)

#### NOICE: script updates will be made from time to time

---

```shell
#!/usr/bin/env bash
# A script to protect your king in KoTH
# Created by @MatheuzSecurity
# https://youtube.com/c/MatheuZSecurity

if [[ $(id -u) -ne "0" ]]; then
        echo "[ERROR] You must run this script as root" >&2
        exit 1
fi

read -p "Put your nickname: " nick

function protectKing() {
	echo $nick > /root/king.txt
	chmod 400 /root/king.txt
	chattr +i /root/king.txt
	set -o noclobber /root/king.txt
}

arr=('.' '..' '...' '....')

for c in $(seq 1); do
        for elt in ${arr[*]}; do
                echo -ne "\r\033[<1>AProtecting your king $elt" && sleep 0.1;
        done
done

echo -ne "\n"

message="Success! Your king has been protected! =D"

for i in $(seq 1 ${#message}); do
        echo -ne "${message:i-1:1}"
        sleep 0.03
done

echo -ne "\n"

clear

function removeChattr(){
	rm /usr/bin/chattr
}

msg="[*] Success! Binary chattr removed! [*]"

for i in $(seq 1 ${#msg}); do
        echo -ne "${msg:i-1:1}"
        sleep 0.03
done
echo -ne "\n"

protectKing && removeChattr /

echo -ne "\n"
```
