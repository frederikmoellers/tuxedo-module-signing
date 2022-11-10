# tuxedo-module-signing
Build, sign and load DKMS modules for Tuxedo laptops with Secure Boot enabled.

## Do I need this?
You do if you:
1. Have a Tuxedo laptop
2. Have Secure Boot enabled
3. Use the DKMS modules supplied by Tuxedo

## How to
1. Place the files in the directory `/root/module-signing` OR adapt the directory in the files where appropriate.
2. Generate a MOK certificate and private key:
```
./one-time-setup
```
3. Make sure the DKMS sources are installed. The package's name is `tuxedo-keyboard`.
4. On every kernel upgrade, run
```
./tuxedo-sign
```
This should take care of building, signing and loading the DKMS modules. Afterwards, you should have all functionality. The quickest way to check is the Tuxedo Control Center. If you see your fan speed, you're good.

## Credits
The `one-time-setup` and `manual-sign` scripts are based on this Gist:
https://gist.github.com/sbueringer/bd8cec239c44d66967cf307d808f10c4

## Can I automate this?
Yes, there are 2 files included for automation: You need to copy `dkms-tuxedo-keyboard.conf` to `/etc/dkms/tuxedo-keyboard.conf` (don't forget to remove the `dkms-` from the filename) and you may need to change the directory where the scripts are located in the same file. Furthermore, your MOK private key must not be passphrase-protected or the automatical signing will fail (or possibly ask for a password on the command line).
