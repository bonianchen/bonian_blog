# Wireless Debug Android Without PC

This is a project regarding having more control over an Android device without rooting it.

### My Target

Within Android, Android Debug Bridge (`adb`) provides a capability (as a `shell` user priviledge) for Android developers to debug and develope.

> `shell` user priviledge allows me to run my backend on an Android device without having too much of the restrictions, and is the candidate I'm looking for.

Therefore, run commands under this condition is my target.

### Issues

To access Android Debug Bridge (`adb`), normally a developer requires a PC to get connect with it either through USB or internet.

> Due to my development of backend software was fully setup on top of an Android device, route command and data out of Android device to a PC and route back again simply for accessing `adb` is over-killing.

Route commands through internet seems to be a good idea to me, however, the wireless debugging feature (introduced since Android 11) enables debugging port only when presenting the pairing information after user clicked the **Pair device with pairing code** button.

> The randomly generated pairing information got dismissed when leaving this **Settings** UI page.

### Workaround Steps

1. Having following apps installed (through [F-Droid](https://f-droid.org/en/)):
* [Termux](https://f-droid.org/en/packages/com.termux/)
* [Termux:API](https://f-droid.org/en/packages/com.termux.api/)
* [Termux:Float](https://f-droid.org/en/packages/com.termux.window/)
* [Termux-adb](https://github.com/nohajc/termux-adb)

2. Adjust **Developer options** within **Settings** app
    * **Allow screen overlays on Settings** : Set to **ON**
    * **Wireless debugging**: Set to **ON**

    ![Sample Screenshot](https://github.com/bonianchen/bonian_blog/blob/main/IMG_20230628_223637.jpg)

3. Close **Settings** app

4. Launch Termux:Float

    A terminal would be float on screen

5. Launch **Settings** app again

    Termux:Float remains stay on top of **Settings** app

6. Clicked the **Pair device with pairing code** button within **Wireless debugging**

    A pop-up dialog show-up with pairing information

7. Move focus to Termux:Float and issue pairing commands:

    `adb pair localhost:[port number] [pair code]`

    `adb connect localhost:[connect port]`

8. Verify the status of pairing

### Troubleshooting

Some users reported unable to pair due to certificate issues
   There're two options which might help:

   1. Get into `~/.android/` folder within Termux (or Termux:Float)
              Issue command: `adb keygen`

   2. Issue command `ps axw` and kill suspicious process as much as possible.
