# How to use sudo in crosh

1. Install netcat using [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation) or any other method (I used `crew install netcat`)
2. In crosh, type `nc -l -p 5050 -vvv`
3. Run `bash -i >& /dev/tcp/127.0.0.1/5050 0>&1` in the VT-2 as chronos (Or, download my [linkterm.sh](https://github.com/OddbyteWasTaken/howto-use-sudo-in-crosh/raw/main/linkterm.sh) so you dont have to type the long command)
4. Enjoy!

### So why do I care about using `sudo` in crosh?
  1. You can open GUI apps as root (like crouton)
  2. You can copy-paste scripts into there, like long install links that you cant be bothered copying letter for letter
  3. You can stick it to chromebook's dev team who disabled sudo in crosh :P
