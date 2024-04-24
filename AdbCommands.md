# ADB Commands Cheat Sheet
https://gist.github.com/mrk-han/4bb41702f317c2534055d30acaa4ff9b


## ADB Server
```bash
adb kill-server
adb start-server
```

## ADB Reboot
```bash
adb reboot
adb reboot recovery
adb reboot bootloader
adb reboot-bootloader
```

## Shell
```bash
adb shell    # Open or run commands in a terminal on the host Android device.
```

## Devices
```bash
adb usb
adb devices    # Show devices attached
adb connect ip_address_of_device
```

## Get Device Android Version
```bash
adb shell getprop ro.build.version.release
```

## LogCat
```bash
adb logcat
adb logcat -c    # clear    The parameter -c will clear the current logs on the device.
adb logcat -d > [path_to_file]    # Save the logcat output to a file on the local system.
adb bugreport > [path_to_file]    # Will dump the whole device information like dumpstate, dumpsys, and logcat output.
```

## Files
```bash
adb push [source] [destination]    # Copy files from your computer to your phone.
adb pull [device file location] [local file location]    # Copy files from your phone to your computer.
```

## App Install
```bash
adb -e install path/to/app.apk
```

## Uninstalling App from Device
```bash
adb uninstall com.myAppPackage
adb uninstall <app .apk name>
adb uninstall -k <app .apk name>    # Uninstall .apk without deleting data
adb shell pm uninstall com.example.MyApp
adb shell pm clear [package]    # Deletes all data associated with a package.
```

## Update App
```bash
adb install -r yourApp.apk    # -r means re-install the app and keep its data on the device.
adb install –k <.apk file path on computer>
```

## Home Button
```bash
adb shell am start -W -c android.intent.category.HOME -a android.intent.action.MAIN
```

## Activity Manager
```bash
adb shell am start -a android.intent.action.VIEW
adb shell am broadcast -a 'my_action'
adb shell am start -a android.intent.action.CALL -d tel:+972527300294    # Make a call
```

## Print Text
```bash
adb shell input text 'Wow, it's so cool feature'
```

## Screenshot
```bash
adb shell screencap -p /sdcard/screenshot.png
```

## Key Event
```bash
adb shell input keyevent 3    # Home btn
adb shell input keyevent 4    # Back btn
adb shell input keyevent 5    # Call
adb shell input keyevent 6    # End call
adb shell input keyevent 26    # Turn Android device ON and OFF. It will toggle the device to on/off status.
adb shell input keyevent 27    # Camera
adb shell input keyevent 64    # Open browser
adb shell input keyevent 66    # Enter
adb shell input keyevent 67    # Delete (backspace)
adb shell input keyevent 207    # Contacts
adb shell input keyevent 220 / 221    # Brightness down/up
adb shell input keyevent 277 / 278 /279    # Cut/Copy/Paste
```

## Shared Preferences
```bash
# replace org.example.app with your application id

# Add a value to default shared preferences.
adb shell 'am broadcast -a org.example.app.sp.PUT --es key key_name --es value "hello world!"'

# Remove a value to default shared preferences.
adb shell 'am broadcast -a org.example.app.sp.REMOVE --es key key_name'

# Clear all default shared preferences.
adb shell 'am broadcast -a org.example.app.sp.CLEAR --es key key_name'

# It's also possible to specify shared preferences file.
adb shell 'am broadcast -a org.example.app.sp.PUT --es name Game --es key level --ei value 10'

# Data types
adb shell 'am broadcast -a org.example.app.sp.PUT --es key string --es value "hello world!"'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key boolean --ez value true'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key float --ef value 3.14159'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key int --ei value 2015'
adb shell 'am broadcast -a org.example.app.sp.PUT --es key long --el value 9223372036854775807'

# Restart application process after making changes
adb shell 'am broadcast -a org.example.app.sp.CLEAR --ez restart true'
```

## Monkey
```bash
adb shell monkey -p com.myAppPackage -v 10000 -s 100    # monkey tool generates 10,000 random events on the real device
```

## Other
```bash
adb backup    # Create a full backup of your phone and save it to the computer.
adb restore    # Restore a backup to your phone.
adb sideload    # Push and flash custom ROMs and zips from your computer.
```

## Wifi
```bash
adb shell svc wifi enable                 # Enable mobile wifi.
adb shell svc wifi disable                 # Disable mobile wifi.
adb shell cmd -w wifi connect-network Public open                 # Connect to an open wifi network.
adb shell cmd -w wifi connect-network Redmi9Prime wpa2 password    # Connect to an secured wifi network.
```

For more advanced

 usage and explanations, please refer to the [ADB documentation](https://developer.android.com/studio/command-line/adb).
