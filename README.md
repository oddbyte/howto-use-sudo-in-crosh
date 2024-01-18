# How to use sudo in crosh
## Method 1: Crosstini with password (Easiest, but a slight security risk)
1. Run `sudo /usr/sbin/sshd` in VT-2 as chronos or root (Control-Alt- ->)
2. In crosstini, run `ssh chronos@localhost` and enter your password.
### Notes on this method:
- You must have a password set for chronos to log in as chronos. To set a password, run `chromeos-setdevpasswd` in VT-2 as root
- You can ssh into root directly by running `ssh root@localhost` in crosstini.
- While this is the simplest method, this is a potential security risk, as you are exposing your ssh port.

## Method 2: Crosstini with ssh-key (Easy)
![Start SSHD](https://github.com/OddbyteWasTaken/howto-use-sudo-in-crosh/assets/141666866/39c5b6d9-41c5-46d5-9264-089d988eb4d8)
1. Run `ssh-keygen` in crosh or VT-2 as chronos
2. Run `cat ~/.ssh/id_ed25519.pub > ~/.ssh/authorized_keys` in crosh
3. Run `sudo /usr/sbin/sshd -oAuthorizedKeysFile=/home/chronos/user/.ssh/authorized_keys` in VT-2 as chronos or root (Control-Alt- ->)
4. In crosstini, run `ssh chronos@localhost` (make sure to copy your ~/.ssh/id_ed25519.pub file to your linux container's ~/.ssh/id_ed25519.pub)
### Notes on this method:
- While this is a simple method, this is a potential security risk, as you are exposing your ssh port.

## Method 3: Netcat and Bash (Medium):
1. Install netcat using [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation) or any other method (I used `crew install netcat`)
2. In crosh, type `nc -l -p 5050 -vvv`
3. Run `bash -i >& /dev/tcp/127.0.0.1/5050 0>&1` in the VT-2 as chronos (Or, download my [linkterm.sh](https://github.com/OddbyteWasTaken/howto-use-sudo-in-crosh/raw/main/linkterm.sh) so you dont have to type the long command)
4. Enjoy!
### Notes on this method:
- Does not expose the ssh port, so is generally preferable.
- Does not need crosstini.

### So why do I care about using `sudo` in crosh?
  1. You can open GUI apps as root (like crouton, or any other app you install using ChromeBrew. I recommend installing sommelier with `chronos@chromebook ~ $ crew install sommelier`)
  2. You can copy-paste scripts into there, like long install links that you cant be bothered copying letter for letter
  3. You can stick it to chromebook's dev team who disabled sudo in crosh :P
