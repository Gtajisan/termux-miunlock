
## termux-miuiunlockr
A program that can be used to retrieve the bootloader unlock token for Xiaomi devices. (and unlock the bootloader) using Termux

**Note: This tool cannot bypass the 7, 14, 30 day unlock time.**

• [How to unlock xiaomi device bootloader using termux?](https://youtu.be/zTArE7sixJI?si=p8m0iQ-D3_abJ_23)
• [modified?](https://github.com/RohitVerma882/termux-miunlock)
## SCREEN SHOTS [Termux]

<br>
<p align="center">
<img width="50%" src="https://i.postimg.cc/65gctdSL/received-1700544700442510.jpg"/>
<img width="46%" src="https://i.postimg.cc/qMVcFkCj/FB-IMG-1698426364938.jpg"/>
</p>




## Usage
```console
Usage: get_token.sh [OPTIONS] DATA
A program that can be used to retrieve the bootloader unlock token for Xiaomi
devices. using Termux.
*     DATA                Install account.apk from repo, login and copy-paste
                            the response.
      --debug             Output messages about what the tool is doing
      --help              Display a help message
*     --product=PRODUCT   Used to verify device product
      --region=REGION     Tool server hosts or regions: india, global, china,
                            russia, europe
                            Default: india
*     --token=TOKEN       Used to verify device token
      --version           Version information
```
### Requirements
* 1) Verified Xiaomi Account.
* 2) Two Android device (Host & Target)
* 3) USB Otg & Data cable.
* 4) Internet Connection.


## some  Instructions
*  Install required apps [termux](https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_arm64-v8a.apk), [termux-api](https://github.com/termux/termux-api) and ```account.apk``` from repo. watch these YouTube video [YouTube](https://youtu.be/zTArE7sixJI?si=Limc8ksk2CyJ--P_) for setup etc.  [mediafire](https://www.mediafire.com/file/1bdsv4ksnebqg8z/MiAccountUnlock.apk/file) for account add

* login and bind your xiaomi account on your target device.
* Clone this repo.

### clone and tool run command Enjoy <😺>

1) setup```setup```command
Agar koi Error aa rha hai tool installation me to ye sabhi pkg install karke fir se try karna:-
```console
pkg update && upgrade && pkg install git && pkg install vim && pkg install curl && pkg install wget

```
3) Clone this repo.
```console
git clone https://github.com/Gtajisan/termux-miuiunlockr.git && cd termux-miuiunlockr && ls
```
3) Run ```setup.sh``` to install required packages.
```console
chmod +x setup.sh && ./setup.sh
```
4) go mi account and login and setup make sure  ```login```
+ and check you're device
```console
mi-fastboot devices
```

6) Get device ```product```
```console
mi-fastboot getvar product
```

6) Get device ```token```
```console
mi-fastboot getvar token
```

7) Get device ```token``` for mtk device.
```console
mi-fastboot oem get_token
```
if you received 2 or 3 token then merge it, 
example:
```console
// Before 
(bootloader) token: VQECMAEQTSdjm281zqPylolzfxy3bQMGbWVy
(bootloader) token: bGluAhTVfQBXJGUJ78qoZQ0ctBDLQ1PkJg==

// After
VQECMAEQTSdjm281zqPylolzfxy3bQMGbWVybGluAhTVfQBXJGUJ78qoZQ0ctBDLQ1PkJg==
```

8) Run ```get_token.sh``` script with required arguments.
```console
chmod +x get_token.sh && ./get_token.sh --product=PRODUCT --token=TOKEN DATA
```
if the code succeeds it will give you a really long string which is the unlock token.

You should pass correct region which you used in account.apk if you got error 20045

available options: `india, global, china, russia, europe, Bangladesh `

```console
chmod +x get_token.sh && ./get_token.sh --product=PRODUCT --region=REGION --token=TOKEN DATA
```

9) Convert unlock token string to binary token.
  ```console
  echo "UNLOCK_TOKEN" | xxd -r -p > token.bin
  ```

10) Type:
```console
mi-fastboot stage token.bin && mi-fastboot oem unlock
```
Or (skip step 8):
```console
mi-fastboot oem-unlock "UNLOCK_TOKEN"
```

The device will factory reset and unlock successfully.
