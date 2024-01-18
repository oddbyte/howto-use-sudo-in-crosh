# How to use sudo in crosh

1. Install netcat using [chromebrew](https://github.com/chromebrew/chromebrew?tab=readme-ov-file#installation) or any other method (I used `crew install netcat`)
2. In crosh, type `nc -l -p 5050 -vvv`
3. Run `bash -i >& /dev/tcp/127.0.0.1/5050 0>&1` in the VT-2 as chronos (or root, chronos is recommended as you can sudo into root if needed)
4. Enjoy!
