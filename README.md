# <img src="https://user-images.githubusercontent.com/70295997/222662992-d2888f51-e3ac-4a90-94f1-aecbcd4fa0d3.png" width=40> [Android Debug Bridge (adb)](https://github.com/lana-20/android-debug-bridge) Commands

ADB commands can be used to debug Android devices, install or uninstall apps, and get information about a connected device. The <code>adb</code> util can practically replicate any action a user performs on the UI.

ADB Shell commands provide access to a Unix Shell that runs a command directly on an Android device. As soon as I execute an <code>adb shell</code> command on the command terminal, it sends a signal to my Android device and triggers the remote shell command console. Thus ADB shell commands let me control my Android device.

Using ADB commands, I can reboot my device, push and pull files, create a backup and restore it, and sideload an updated zip package or an APK. ADB Shell commands, however, work on a much deeper level. They can be used to change the resolution of my device display, uninstall bloatware or system apps, enable and disable features, modify the system files, and change their configuration directly using commands from my computer.

Here is a list of some common ADB (Android Debug Bridge) commands that I use frequently as a mobile QA engineer:	
	
✰ <code>adb devices -l</code> - Lists all the devices that are connected to my computer and are recognized by ADB. To make sure the device I'm planning to manipulate is actually connected, I always start with the command <code>adb devices</code> and then issue my next adb command.

- For example, confirm that the host computer is connected to the target device:
	
        $ adb devices
        List of devices attached
        device_ip_address:5555 device
	
✰ [<code>adb push <local_file> <remote_destination></code>](https://github.com/lana-20/mobile-testing-interview-questions#:~:text=adb%20push%20%3Clocal_file%3E%20%3Cremote_destination%3E) - Copies a file, or directory and its sub-directories, from my computer to the connected device.
	
- For example:
	
        adb push myfile.txt /sdcard/myfile.txt
	
✰ <code>adb pull <remote_file> <local_location></code> - Copies a file, or a directory and its sub-directories, from the connected device to my computer.

✰ <code>adb logcat</code> - Displays the logcat output for the connected device, which can be helpful for debugging.

✰ <code>adb shell</code> - Opens a shell on the connected device, allowing me to run commands on the device directly.
	
✰ <code>adb shell dumpsys <system_service></code> - Displays detailed information about a specific system service on the device.
	
✰ <code>adb -d shell ip addr show wlan0</code> - Finds the device's IP address. Alternatively, I can search in the phone settings.
	
✰ <code>adb tcpip 5555</code> - Sets the target device to listen for a TCP/IP connection on port 5555.
	
✰ <code>adb connect device_ip_address:5555</code> - Connects to the device by its IP address.
	
✰ <code>adb start-server</code> - Starts the adb server.
	
✰ <code>adb kill-server</code> - Resets the adb host / Stops the adb server. In some cases, I need to terminate the adb server process and then restart it to resolve a problem (e.g., if adb does not respond to a command). After stopping, I can then restart the server by issuing any adb command.

✰ <code>adb reboot</code> - Reboots the connected device.

✰ <code>adb --help</code> - Yields a detailed list of all supported adb commands.

These are just a few examples of the many ADB commands that are available. In the following section, I cover some of the commands I use as a mobile tester most frequently.
	
## <img src="https://user-images.githubusercontent.com/70295997/222727852-07d04327-0a1d-4ae8-ac79-1a6ba8aebebd.png" width=40> Install, Update, Uninstall an App	

✰ [<code>adb install ~/apks/my_app.apk</code>](https://github.com/lana-20/mobile-testing-interview-questions#if-you-have-several-android-devices-virtual-emulators-andor-physical-phones-connected-to-your-machine-how-do-you-install-an-application) - Installs an app (specified by the APK file path) on a **single** connected device.

✰ [<code>adb devices | grep device | grep -v devices | cut -f 1 | xargs -I {} adb -s {} install ~/apks/my_app.apk</code>](https://stackoverflow.com/questions/8610733/how-can-i-adb-install-an-apk-to-multiple-connected-devices) - Installs an app (specified by the APK file) on **multiple** connected devices.
	
✰ [<code>adb install -r Downloads/<file_name>.apk</code>](https://github.com/lana-20/mobile-testing-interview-questions#if-you-have-an-old-version-installed-and-you-dont-want-to-lose-your-data-how-you-install-a-new-apk-file) - Reinstalls an (updated) app on the connected device. Add <code>-r</code> **before** the path to .apk.
	
✰ [<code>adb uninstall <package_name></code>](https://github.com/lana-20/mobile-testing-interview-questions#how-do-you-uninstall-an-application) - Uninstalls an app by its package name from the connected device.

## <img src="https://user-images.githubusercontent.com/70295997/222729738-d7fccced-5c0a-49c2-96c0-6cf03cdfb6c9.png" width=40> Command Redirection
✰ <code>adb -d <command></code> - Sends a command to the **only** connected physical device (CONNECTED via USB).
	
✰ <code>adb -e <command></code> - Sends a command to the **only** connected emulator (CONNECTED via TCP/IP).
	
Once a physical device is connected via TCP/IP, use the <code>-e</code> or <code>-s <serial_number></code> redirection option, since <code>-d</code> sends a command to devices connected via USB.
	
✰ <code>adb -s <serial_number> <command></code> - Use if more than one device or more than one emulator are connected.
	
- For example:
	
        adb -s emulator-5554 install my_app.apk
	
## <img src="https://user-images.githubusercontent.com/70295997/222664101-9da4621a-2457-4f28-b3a4-291a1eef9505.png" width=40> ADB Shell Commands
ADB Shell commands provide access to a Unix Shell that runs a command directly on my Android device. As soon as I execute an <code>adb shell</code> command on the command terminal, it sends a signal to my Android device and triggers the remote shell command console. Thus ADB shell commands let me control my Android device.
	
✰ <code>adb [-d | -e | -s serial_number] shell</code> - Uses the shell command to start an interactive shell through adb.
	
✰ <code>adb [-d |-e | -s serial_number] shell <shell_command></code> - Uses the shell command to issue device commands through adb.
	
✰ <code>adb shell ls /system/bin</code> - Lists available [Unix/Linux-like] CLI tools.
	
✰ <code>adb shell getprop</code> - Returns the list of the device's properties; can be useful when I need to get, e.g., a device model or an Android version.	
	
✰ <code>adb shell getprop ro.build.version.release</code> - Returns the Android version installed on the device, e.g., Android 13.0.
	
✰ <code>adb shell getprop ro.build.version.sdk</code> - Returns the API level, e.g., 33.
	
✰ <code>adb shell am</code> - Issues commands with (calls) the Activity Manager <code>am</code> tool to perform various system actions, such as start an activity, force-stop a process, broadcast an intent, modify the device screen properties, etc.
	
- For example:
	
        adb shell am start -a android.intent.action.VIEW
	
- Or, force-close the app:
	
		adb shell am force-stop com.my_app.standalone.test2

- Or, start the app - need to know the app's 1st activity created on launch:
	
		adb shell am start <package_name>/<activity_name>
		adb shell am start com.my_app.standalone.test2/com.my_app.standalone.features.auth.AuthActivity

✰ <code>adb shell pm</code> - Issues commands with (calls) the Package Manager <code>pm</code> tool to perform actions and queries on app packages installed on the device.
	
- For example:
	
        adb shell pm uninstall com.example.MyApp
	
- Or, clear all package data from the device - after running this command, the app behaves as if it was just installed:
	
		adb shell pm clear com.my_app.standalone.test2


✰ <code>adb shell dpm</code> - Issues commands with (calls) the Device Policy Manager <code>dpm</code> tool to control the active admin app or change a policy's status data on the device.
	
- For example:
	
        adb shell dpm force-network-logs

✰ <code>adb shell cmd testharness enable</code> - Resets test devices between tests, e.g., to remove user data and reset the test environment.
	
✰ <code>adb shell sqlite3 db_location</code> - sqlite CLI program for examining SQLite databases.
	
- For example:
	
        $ adb -s emulator-5554 shell
        $ sqlite3 /data/data/com.example.app/databases/rssitems.db
        SQLite version 3.3.12
        Enter ".help" for instructions
	
✰ <code>adb shell monkey -p <package_name> -v 500</code> - Performs 500 random interactions on the given app. [Monkey](https://developer.android.com/studio/test/monkey) is a program that runs on your emulator or device and generates pseudo-random streams of user events such as clicks, touches, or gestures, as well as a number of system-level events. The tool is useful for stress/interruption testing.

	
- For example, send 1000 random clicks and touches to the app:
	
        adb shell monkey -p com.appiumpro.the_app -v 1000
	
✰ <code>exit</code> - Exits an interactive shell.
	
## <img src="https://user-images.githubusercontent.com/70295997/222665055-a70b67a5-bd18-4359-b08a-18523b7e7d2c.png" width=40> Take a screenshot
✰ <code>adb shell screencap file_name.png</code>
  - For example:
	- <code>adb shell screencap /sdcard/screenshot.png</code>
		- saves the screenshot to the device's SD card - must always state the .png format explicitly
	- <code>adb shell screencap -p > ~/Desktop/screenshot.png</code>
		- <code>-p</code> forces <code>screencap</code> to use PNG format

	<img width=30 src="https://user-images.githubusercontent.com/70295997/222704599-be2a4adb-ddf1-4934-be42-f789effbc134.png"> Alternatively, I can take a screenshot using (1) emulator settings and (2) in Android Studio (under Logcat) with buttons.

## <img src="https://user-images.githubusercontent.com/70295997/222665494-0f62d00d-cf8e-4e8a-904c-a2ec8a0d12d5.png" width=40> Record a video
✰ <code>adb shell screenrecord [options] file_name.mp4</code>
 - For example:
	- <code>adb shell screenrecord /sdcard/ErrorMsgRegistrationScreen.mp4</code>
	
	Or, split the command into several steps:

			$ adb shell
			shell@ $ screenrecord --verbose /sdcard/demo.mp4
			(press Control + C to stop)
			shell@ $ exit
			$ adb pull /sdcard/demo.mp4

	✘ Give the file a meaningful name, e.g., use a bug number as a file name.
	
	💥 Limitations:
	
	1. 🔇 The recording has no audio sound.	
	2. ⏳ The recording time limit is 180 seconds (3 minutes). I may, however, change that by adding the <code>--time-limit</code> argument. I can use the <code>--time</code> shortcut in lieu of the <code>--time-limit</code>.
	
			adb shell screenrecord --time-limit <TIME> /sdcard/ErrorMsgRegistrationScreen.mp4
 		- For example, produce a 2-minute video:
	
				adb shell screenrecord --time 120 /sdcard/ErrorMsgRegistrationScreen.mp4

	<img width=30 src="https://user-images.githubusercontent.com/70295997/222704143-3af9a5c0-81af-43bf-9078-2f983621db17.png"> Since the video is saved to the SD card, I need to <code>pull</code> it from the device to my current working directory:
			
		adb pull /sdcard/ErrorMsgRegistrationScreen.mp4
	
	Or, pull to a specified destination:
			
		adb pull /sdcard/ErrorMsgRegistrationScreen.mp4 ~/Desktop
	
	If no destination directory is specified, the file is stored at my current working directory. To check the current directory location, use command <code>pwd</code> on Mac or <code>cd</code> on Windows.

	❌ To remove a file from the device, run the <code>rm</code> command:
			
		adb shell rm /sdcard/ErrorMsgRegistrationScreen.mp4
	
	<img width=30 src="https://user-images.githubusercontent.com/70295997/222704599-be2a4adb-ddf1-4934-be42-f789effbc134.png"> Alternatively, I can [record a video in Android Studio](https://developer.android.com/studio/debug/am-video.html?hl=en).


## <img src="https://user-images.githubusercontent.com/70295997/222664496-9662aacc-8f0a-492d-b2f6-6821f597527b.png" width=40> [Battery and Power](https://developer.android.com/studio/command-line/dumpsys#battery)
<code>dumpsys</code> is a tool which runs on Android devices and provides information about system services. Sometimes it's helpful for retrieving info about the device memory or battery usage.

__List options available with dumpsys__
- _adb shell dumpsys | grep "DUMP OF SERVICE"_

__Check the current status of the phone__
- _adb shell dumpsys battery_

        $ adb shell dumpsys battery
          USB powered: true
          
        $ adb shell dumpsys battery unplug
                
        $ adb shell dumpsys battery
          USB powered: false

__Change battery level__
- _adb shell dumpsys battery set level <battery_percent_value>_
  - eg, _adb shell dumpsys battery set level 20_
  
__Test how the device behaves under low power conditions__
- _adb shell settings put global low_power 1_

__Mimic a disabled battery charge__
- _adb shell dumpsys battery unplug_
  - only MOCKS the battery status. When checking the current indicator on the USB cable, this does not change the amount of flowing current at all. So the battery is still charging. It only changes what apps think about the state. Eg, Google Play would not start updating, if you have configured that it can only update when charging.

        $ adb shell dumpsys battery unplug

        $ adb shell service list | grep battery
        88      batterymanager: [android.app.IBatteryService]
        107     batterystats: [com.android.internal.app.IBatteryStats]
        114     batteryproperties: [android.os.IBatteryPropertiesRegistrar]

        $ adb shell dumpsys batterymanager

        Current Battery Service state:
          (UPDATES STOPPED -- use 'reset' to restart)
          AC powered: false
          USB powered: true

        $ adb shell dumpsys batterymanager unplug

        Current Battery Service state:
          (UPDATES STOPPED -- use 'reset' to restart)
          AC powered: false
          USB powered: false

__For a rooted device:__
- Enable battery Charging (mimic that device is charging, event if it's not -> simulate the uncharged state of the phone)
  - _adb shell dumpsys battery set ac 1_
  - _adb shell dumpsys battery set usb 1_
  - _adb shell dumpsys battery set wireless 1_

- Disable battery Charging (mimic that device isn't charging, event if it is)
   - _adb shell dumpsys battery set ac 0_
   - _adb shell dumpsys battery set usb 0_
   - _adb shell dumpsys battery set wireless 0_

__Restore the phone to its state__
- _adb shell dumpsys battery reset_

## <img src="https://user-images.githubusercontent.com/70295997/222664856-1274022a-decf-42cf-bc43-c837c883ecf5.png" width=40> [Memory Allocations](https://developer.android.com/studio/command-line/dumpsys#ViewingAllocations)

Inspect an app's memory usage in one of two ways: 
1. Over a period of time using <code>procstats</code>.
- Get application memory usage stats over the last three hours, in human-readable format
   - _adb shell dumpsys procstats --hours 3_
2. At a particular point in time using <code>meminfo</code>.
- Record a snapshot of how the app's memory is divided between different types of RAM allocation
   - _adb shell dumpsys meminfo package_name|pid [-d]_
   
   The <code>-d</code> flag prints more info related to Dalvik and ART memory usage. The output lists all of your app's current allocations, measured in KBs.

The output lists all of the app's current allocations, measured in kilobytes.
	
## <img src="https://user-images.githubusercontent.com/70295997/222684527-c0f7569d-2c87-408c-a2e1-795af0695a83.png" width=40> Find App Package Name
Review the ADB and AAPT approaches [here](https://github.com/lana-20/android-package-name).
	
----

[dumpsys](https://developer.android.com/studio/command-line/dumpsys)

[Test power-related issues](https://developer.android.com/topic/performance/power/test-power)

[Test apps on Android ](https://developer.android.com/training/testing)

[What to test in Android](https://developer.android.com/training/testing/fundamentals/what-to-test)

[How to disable battery charging during ADB connection?](https://stackoverflow.com/questions/30731921/how-to-disable-battery-charging-during-adb-connection)

[Android Command-line tools](https://developer.android.com/studio/command-line)

[Enter Doze Mode With Adb](https://jubin.tech/articles/2019/01/04/Enter-doze-mode-with-adb.html)

[Optimize for Doze and App Standby](https://developer.android.com/training/monitoring-device-state/doze-standby)

[Android Doze mode is enabled and restored using commands](https://blog.csdn.net/zyp009/article/details/78456906)

[ADB Shell Commands List and Detailed Cheat Sheet](https://technastic.com/adb-shell-commands-list/)
