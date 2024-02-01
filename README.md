# How to use sudo without opening VT-2

### These methods will help you be able to copy paste stuff into terminals in ChromeOS.

## Method 1: XFCE4-Terminal (super easy)
1. Install [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation)
2. Run `crew install xfce4_terminal && crew install sommelier`
3. Run `xfce4-terminal` in VT-2 as chronos or root (Control-Alt- ->)
4. Enjoy!

## Method 2: Crosstini with password (Easy, but a slight security risk)
1. Run `sudo /usr/sbin/sshd -p 6969` in VT-2 as chronos or root (Control-Alt- ->)
2. In crosstini, run `ssh chronos@localhost -p 6969` and enter your password.
### Notes on this method:
- You must have a password set for chronos to log in as chronos. To set a password, run `chromeos-setdevpasswd` in VT-2 as root
- You can ssh into root directly by running `ssh root@localhost` in crosstini.
- While this is the simplest method, this is a potential security risk, as you are exposing your ssh port.

## Method 3: Crosstini with ssh-key (Easy, but a slight security risk)
![Start SSHD](https://github.com/OddbyteWasTaken/howto-use-sudo-in-crosh/assets/141666866/39c5b6d9-41c5-46d5-9264-089d988eb4d8)
1. Run `ssh-keygen` in crosh or VT-2 as chronos
2. Run `cat ~/.ssh/id_ed25519.pub > ~/.ssh/authorized_keys` in crosh
3. Run `sudo /usr/sbin/sshd -oAuthorizedKeysFile=/home/chronos/user/.ssh/authorized_keys -p 6969` in VT-2 as chronos or root (Control-Alt- ->)
4. In crosstini, run `ssh chronos@localhost -6969` (make sure to copy your ~/.ssh/id_ed25519.pub file to your linux container's ~/.ssh/id_ed25519.pub)
### Notes on this method:
- While this is a simple method, this is a potential security risk, as you are exposing your ssh port.

## Method 4: Netcat and Bash (Medium):
1. Install netcat using [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation) or any other method (I used `crew install netcat`)
2. In crosh, type `shell`
3. In the crosh shell window, type `nc -l -p 5050 -vvv`
4. Run `bash -i >& /dev/tcp/127.0.0.1/5050 0>&1` in the VT-2 as chronos (Or, download my [linkterm.sh](https://github.com/OddbyteWasTaken/howto-use-sudo-in-crosh/raw/main/linkterm.sh) so you dont have to type the long command)
5. Enjoy!
### Notes on this method:
- Does not expose the ssh port, so is generally preferable.
- Does not need crosstini.

## Method 5: Using GPP and a bunch of other stuff to get crosh to run sudo
follow [this tutorial](https://gist.github.com/CoolElectronics/a5088c9ade6ec4d35435b9826b45d7a3)

### Notes on this method:
- Makes Crosh itself be able to use sudo without using netcat or VT2 or whatever.
- Stops working after updating.
- Needs crosstini (Or [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation) with `crew install buildessential` to install GPP)
- Is hard to type all of the stuffs perfectly into VT-2
- Is meh method overall, will make your chromebook not be able to show the desktop or make u powerwash it if you misstype even one letter in some of the commands, and it resets on updates. Use method one cause easy. However, it is the most User-Friendly after you set it up, as it uses actual crosh which has tabs and stuff and you dont need to use VT-2, as long as you know how to keep re-setting it every time you update.

### So why do I care about using `sudo` in crosh?
  1. You can open GUI apps as root (like crouton, or any other app you install using ChromeBrew. I recommend installing sommelier with `chronos@chromebook ~ $ crew install sommelier`)
  2. You can copy-paste scripts into there, like long install links that you cant be bothered copying letter for letter
  3. You can stick it to chromebook's dev team who disabled sudo in crosh :P
