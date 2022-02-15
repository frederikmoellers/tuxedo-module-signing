# tuxedo-module-signing
Build, sign and load DKMS modules for Tuxedo laptops with Secure Boot enabled.

## Do I need this?
You do if you:
1. Have a Tuxedo laptop
2. Have Secure Boot enabled
3. Use the DKMS modules supplied by Tuxedo

## How to
1. Generate a MOK certificate and private key:
```
./one-time-setup
```
2. Make sure the DKMS sources are installed. The package's name is `tuxedo-keyboard`.
3. On every kernel upgrade, run
```
./tuxedo-sign
```
This should take care of building, signing and loading the DKMS modules. Afterwards, you should have all functionality. The quickest way to check is the Tuxedo Control Center. If you see your fan speed, you're good.

## Credits
The `one-time-setup` and `manual-sign` scripts are based on this Gist:
https://gist.github.com/sbueringer/bd8cec239c44d66967cf307d808f10c4

## Can I automate this?
Sure, it should be possible. Consult the Gist and the linked repository there, they include instructions how to make DKMS sign all modules automatically. However, note that if you need to enter a passphrase for the MOK private key, you need a way to do so during package upgrades. This might not be trivial, e.g. if you use the "Software Updates" tray app in KDE or any other graphical frontend. It's certainly possible and you're welcome to submit a PR if you have done so :)
