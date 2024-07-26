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
adb reboot -p
adb shell reboot -p
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
adb devices                      # Show devices attached
adb -s serial_id_of_device       # Connect to an adb devices 
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
adb shell svc wifi enable                  # Enable mobile wifi.
adb shell svc wifi disable                 # Disable mobile wifi.
adb shell cmd -w wifi connect-network Public open                  # Connect to an open wifi network.
adb shell cmd -w wifi connect-network Redmi9Prime wpa2 password    # Connect to an secured wifi network.
```

## Enable hotspot tethering
The first command opens the Settings page for Tethering and Hotspot, while the latter simulate key presses: Down and Enter, respectively.
```bash
adb shell am start -n com.android.settings/.TetherSettings
adb shell input keyevent 20     # Press Down
adb shell input keyevent 66     # Press Enter 
```

## Unlock pin screen lock
```bash
adb shell input keyevent 82     # 1. Pressing the lock button
adb shell input keyevent 66     # 2. Pressing the lock button
adb shell input keyevent 26     # 3. Pressing the lock button
adb shell input touchscreen swipe 930 880 930 380      # Swipe UP
adb shell input text XXXX       # Entering your passcode
adb shell input keyevent 66     # Pressing Enter
```

## Root Commands
```bash
adb shell "su -c ls"   # list working directory with su rights.
adb shell "su -c echo anytext > /data/test.file"
```

## Set system-level preferences
```bash
adb shell settings put secure location_mode 0                   # Enable (Value: 3) / Disable (Value: 0) location.
adb shell settings put global heads_up_notifications_enabled 0  # Enable (Value: 1) / Disable (Value: 0) pop-up notifications.
adb shell settings put global always_finish_activities 0        # Enable (Value: 1) / Disable (Value: 0) aggressive finishing of activities and processes.
adb shell settings put system accelerometer_rotation 0          # Enable (Value: 1) / Disable (Value: 0) auto-rotation of the device.
adb shell settings put system user_rotation 3                   # (0° rotation: 0 / 90° rotation: 1 / 180° rotation: 2 / 270°  rotation: 3) clockwise rotate the device.
```

## Get system and device properties using getprop
```bash
adb shell getprop -T        # Provides a list of system property types. (Important: this command can only be used on Android version 8.1 and above.)
adb shell getprop gsm.sim.operator.alpha         # Provides SIM Operator
adb shell getprop ro.build.version.release       # Provides device android version
adb shell getprop ro.boot.wifimacaddr            # Provides the WiFi Mac Address
adb shell getprop ro.product.manufacturer        # Provides Android device manufacturer details
adb shell getprop ro.vendor.product.model        # Provides Android device product number
adb shell getprop ro.board.platform              # Provides Soc info
adb shell getprop ro.oem_unlock_supported        # Provides OEM unlock status
adb shell getprop ro.vendor.product.model        # Provides device model
adb shell getprop ro.bootimage.build.fingerprint # Provides Android device build fingerprint
adb shell getprop ro.cdma.home.operator.alpha    # Provides SIM operator name
adb shell getprop ro.system.build.version.sdk    # Provides API level
```

## Get diagnostic output for system services using dumpsys
[dumpsys](https://developer.android.com/studio/command-line/dumpsys) is a tool that runs on Android devices and offers information on system services. adb shell dumpsys commands provide vital diagnostic output for system services operating on a connected device

** Activities
```bash
adb shell dumpsys activity -p <package_name>   # Provides complete activity history for the given package
adb shell dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'  # Prints current app’s opened activity
adb shell dumpsys activity -p <package_name> activities  # Provides activity manager activities that contain main stack, running activities, and recent tasks
adb shell dumpsys activity -p <package_name> activities | grep -E 'mResumedActivity'  # Prints current app’s resumed activity
adb shell dumpsys activity -p <package_name> services  # Provides list of services running for the given package
adb shell dumpsys activity -p <package_name> providers  # Provides list of current content providers for the given package
adb shell dumpsys activity -p <package_name> recents  # Provides list of recent tasks for the given package
adb shell dumpsys activity -p <package_name> broadcasts  # Provides list of broadcast states for the given package
adb shell dumpsys activity -p <package_name> intents  # Provides list of pending intents for the given package
adb shell dumpsys activity -p <package_name> permissions  # Provides list of permissions for the given package
adb shell dumpsys activity -p <package_name> processes  # Provides list of running processes for the given package
```

** Device
```bash
adb shell dumpsys cpuinfo   # Provides info on CPU usage
adb shell dumpsys display   # Provides info on display
adb shell dumpsys power     # Provides info on power statistics
adb shell dumpsys alarm     # Provides info on alarm
adb shell dumpsys location  # Provides info on location
adb shell dumpsys window displays     # Provides info like pixel resolution, FPS, and DPI of the device’s display
adb shell dumpsys telephony.registry  # Gives information about wireless communication related parameters
adb shell dumpsys bluetooth_manager   # Gives information about connected bluetooth devices, mac addresses etc.
```

** Networks
```bash
adb shell dumpsys connectivity         # Provides the internet status and connectivity mode(cellular or Wi-Fi)
adb shell dumpsys network_management   # Provides all information about device network management
```

** Package
```bash
adb shell dumpsys package <package_name>   # Provides all the info about your app, ex: Version name/code, first install time, requested permissions, etc
```

** Input
```bash
adb shell dumpsys input      # Dumps the state of the system’s input devices, such as keyboards and touchscreens, and the processing of input events
```

## For more advanced

 Usage and explanations, please refer to the [ADB documentation](https://developer.android.com/studio/command-line/adb).
 <br> Addintional resources.
 <br> [1] <https://newandroidbook.com/ddb/S23/>
 
