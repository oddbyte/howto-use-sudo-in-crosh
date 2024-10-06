# How to use sudo without opening VT-2

### These methods will help you be able to copy paste stuff into terminals in ChromeOS.
### These methods only work if your chromebook is in developer mode :|

## Method 1: Crew-sudo (super easy, recommended method)
1. Get into VT-2 (Control-Alt-Forward arrow button thing (looks like **->**))
2. Install [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation)
3. Run `crew install crew-sudo`
4. Sign out of VT2, sign back into VT2 as chronos and wait for crew-sudo to start.
5. Go back to the main screen using Control-Alt-Back arrow
6. Open Crosh, and enter shell.
7. Type `sudo bash` to get into a root shell. If it doesn't work, follow the instructions it gives, and if it says not found then you installed it wrong.
8. Profit

### Notes on this method:
- You will need to log into chronos in VT2 on every reboot to restart crew-sudo.
- This is the easiest method, and doesn't need you to mess around with sommelier.

## Method 2: XFCE4-Terminal (very easy)
1. Install [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation)
2. Run `crew install sommelier xfce4_terminal`
3. Run `xfce4-terminal` in VT-2 as chronos or root (Control-Alt- ->)
4. Enjoy!

### Notes on this method:
- The window doesn't look as nice as normal crosh
- Requires sommelier (which is kinda jank)

## Method 3: Crosstini with password (Easy, but a slight security risk)
1. Run `sudo /usr/sbin/sshd -p 6969` in VT-2 as chronos or root (Control-Alt- ->)
2. In crosstini, run `ssh chronos@localhost -p 6969` and enter your password.
### Notes on this method:
- You must have a password set for chronos to log in as chronos. To set a password, run `chromeos-setdevpasswd` in VT-2 as root
- You can ssh into root directly by running `ssh root@localhost` in crosstini.
- While this is the simplest method, this is a potential security risk, as you are exposing your ssh port.

## Method 4: Crosstini with ssh-key (Easy, but a slight security risk)
![Start SSHD](https://github.com/OddbyteWasTaken/howto-use-sudo-in-crosh/assets/141666866/39c5b6d9-41c5-46d5-9264-089d988eb4d8)
1. Run `ssh-keygen` in crosh or VT-2 as chronos
2. Run `cat ~/.ssh/id_ed25519.pub > ~/.ssh/authorized_keys` in crosh
3. Run `sudo /usr/sbin/sshd -oAuthorizedKeysFile=/home/chronos/user/.ssh/authorized_keys -p 6969` in VT-2 as chronos or root (Control-Alt- ->)
4. In crosstini, run `ssh chronos@localhost -6969` (make sure to copy your ~/.ssh/id_ed25519.pub file to your linux container's ~/.ssh/id_ed25519.pub)
### Notes on this method:
- While this is a simple method, this is a potential security risk, as you are exposing your ssh port.

## Method 5: Using GPP and a bunch of other stuff to get crosh to run sudo natively (hard)
follow [this tutorial](https://gist.github.com/velzie/a5088c9ade6ec4d35435b9826b45d7a3)

### Notes on this method:
- Makes Crosh itself be able to use sudo without using netcat or VT2 or whatever.
- Stops working after updating.
- Needs crosstini (Or [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation) with `crew install buildessential` to install GPP)
- Is hard to type all of the stuffs perfectly into VT-2
- Is meh method overall (especially because Method 1 achieves the same thing but a lot easier), will make your chromebook not be able to show the desktop or make u powerwash it if you misstype even one letter in some of the commands, and it resets on updates. Use method one cause easy. However, it is the most User-Friendly after you set it up, as it uses actual crosh which has tabs and stuff and you dont need to use VT-2, as long as you know how to keep re-setting it every time you update.

### So why do I care about using `sudo` in crosh?
  1. You can open GUI apps as root (like crouton, or any other app you install using ChromeBrew. I recommend installing sommelier with `chronos@chromebook ~ $ crew install sommelier`)
  2. You can copy-paste scripts into there, like long install links that you cant be bothered copying letter for letter
  3. You can stick it to chromebook's dev team who disabled sudo in crosh :P
