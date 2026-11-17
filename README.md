# **AYANEO Pocket DS – Rooting & Unrooting Guide**

This guide explains how to obtain root access on your AYANEO Pocket DS.

All the files required for the rooting process are included in this repository.

Download and extract all the files to a folder on your computer before getting started.

## **Part 1 – Preparing Your Device**

**Step 1. Install USB Drivers**

Download and install the Windows USB drivers included in the downloaded files.

**Step 2. Create a Rooting Folder**

Connect your AYANEO Pocket DS to your computer.

Using Windows File Explorer, navigate to the device's internal storage and create a folder named `rooting` inside the `Download` directory.

The folder path should look like this:

```
This PC\Pocket DS\Internal shared storage\Download\rooting
```
<img width="1149" height="187" alt="image" src="https://github.com/user-attachments/assets/4d5ce33d-141e-4d5d-bc07-6c0ad1dd2ee6" />


**Step 3. Extract the Original Boot Images**

Copy the file `dump init boot.txt` into the newly created `rooting` folder.

On your Pocket DS, open:

`AYA Settings > Device > Root Script`

<img width="997" height="442" alt="image" src="https://github.com/user-attachments/assets/8f1bc232-ff8d-45bd-a06f-9de022ac43b5" />


Select the `dump init boot.txt` file that you copied to the device.

Press **Run**.
<img width="1002" height="556" alt="image" src="https://github.com/user-attachments/assets/01833e58-c4a1-4c58-818e-4b6650574aa4" />


After pressing Run, the device should confirm that two files have been extracted:

- `init_boot_a.img`
- `init_boot_b.img`

<img width="1002" height="554" alt="image" src="https://github.com/user-attachments/assets/d909a318-009c-4ee4-993a-8d2ec0382ce1" />


These files will be saved in the root directory of your Pocket DS internal storage.
<img width="848" height="234" alt="image" src="https://github.com/user-attachments/assets/70beddfe-35ea-41b8-a10d-640ca0d9afe3" />

Copy both files to your computer and keep them somewhere safe.



Important

&#x20;These are your original boot images. You will need them if you ever want to remove root access and restore your device to its original state.



**Step 4. Install Magisk**

Install Magisk using the APK file included in the downloaded files.

## **Part 2 – Enable Developer Options**

**Step 1. Enable Developer Mode**

On your Pocket DS, open the main Android Settings.

1. Scroll down to the last category, **About device**.
2. Find the **Build number** entry.
3. Tap it repeatedly until the system confirms that Developer Mode has been enabled.

<img width="1920" height="1080" alt="PocketHub_1794927323131_top" src="https://github.com/user-attachments/assets/db460298-ce34-456a-8d30-7884e493c54b" />
<img width="1920" height="1080" alt="PocketHub_1794927330847_top" src="https://github.com/user-attachments/assets/a2e12afc-772e-434e-899b-4507dedd1299" />



**Step 2. Enable USB Debugging**

1. Return to the main Settings menu.
2. Open **System**.
3. You should now see **Developer options**.
4. Open Developer options and enable **USB debugging**.

<img width="1920" height="1080" alt="PocketHub_1794927391950_top" src="https://github.com/user-attachments/assets/bc938061-41cd-4a67-ac07-f062e85371ec" />
<img width="1920" height="1080" alt="PocketHub_1794927407819_top" src="https://github.com/user-attachments/assets/6fac77a4-d865-4145-bd59-57f67f8be742" />


## **Part 3 – Identify Your Active Boot Slot**

**Step 1. Open Platform Tools**

On your computer, extract the archive:

`platform-tools-latest-windows.zip`

Open the extracted `platform-tools` folder.

Click the address bar in Windows File Explorer, type:

```
cmd
```
<img width="931" height="610" alt="image" src="https://github.com/user-attachments/assets/67de79ae-9270-4879-88d1-54a93dd47e3c" />


Press Enter to open Command Prompt in this folder.

**Step 2. Check the ADB Connection**

Connect your Pocket DS to your computer (if it is not already connected).

In Command Prompt, enter:

```
adb devices
```

Make sure your Pocket DS appears in the device list.

If your device asks for permission to allow USB debugging, accept the request.

**Step 3. Enter Fastboot Mode**

Enter:

```
adb reboot fastboot
```

<img width="922" height="547" alt="image" src="https://github.com/user-attachments/assets/3418703d-c322-4920-bc9b-9e4aee5fa552" />


Your Pocket DS will reboot into Fastboot mode.

**Step 4. Verify the Fastboot Connection**

Enter:

```
fastboot devices
```

Make sure your device is listed.

**Step 5. Identify the Active Slot**

Enter:

```
fastboot getvar current-slot
```

<img width="927" height="502" alt="image" src="https://github.com/user-attachments/assets/7d8cb340-b36d-4269-baaf-2952d3ecc9ee" />


The command will tell you which boot slot is currently active.

For example:

```
current-slot: b
```

In this example, the active slot is **B**, so we need to patch the `init_boot_b.img` file.

<img width="915" height="469" alt="image" src="https://github.com/user-attachments/assets/6714c7f4-00ce-4a5f-b99b-1c97d9b2d0a7" />


Important

&#x20;Remember whether your device reports slot **A** or **B**. Your device may report either one. Do not automatically assume it will be B!



**Step 6. Reboot Your Device**

Enter:

```
fastboot reboot
```

Your Pocket DS will reboot into Android.

## **Part 4 – Patch the Boot Image Using Magisk**

Open Magisk on your Pocket DS.

1. Press **Install**.
2. Select **Select and Patch a File**.
3. Navigate to the location where you copied your original boot images.
4. Select the image corresponding to your active slot.

<img width="924" height="456" alt="image" src="https://github.com/user-attachments/assets/a06f10e7-61f1-4c6f-963f-ccbac99e38e2" />

<img width="995" height="565" alt="image" src="https://github.com/user-attachments/assets/07e9c06c-333b-4809-8238-538196a520e6" />
<img width="1002" height="554" alt="image" src="https://github.com/user-attachments/assets/1727d61a-6730-4bf2-a366-ee4e0cbc5587" />



For example:

- If your active slot is **B**, select `init_boot_b.img`.
- If your active slot is **A**, select `init_boot_a.img`.



Important

&#x20;Make sure you select the correct image. It must match the active slot identified earlier.



Magisk will now patch the selected image and create a new patched file, usually named something similar to:

`magisk_patched-xxxxx.img`

Copy this patched file to the `platform-tools` folder on your computer.

<img width="815" height="521" alt="image" src="https://github.com/user-attachments/assets/a431c597-a6be-4266-9b64-fd87870504b5" />


Rename the file according to your active slot:

- Slot B: `init_boot_b.img`
- Slot A: `init_boot_a.img`

<img width="819" height="521" alt="image" src="https://github.com/user-attachments/assets/aa0d3348-ba99-4925-85d5-5ab34d0e5955" />


## **Part 5 – Flash the Patched Image**

**Step 1. Enter Fastboot Mode Again**

<img width="946" height="465" alt="image" src="https://github.com/user-attachments/assets/d71060f8-55fd-4867-88bf-44b4332adcff" />


In the Command Prompt window on your computer, enter:

```
adb reboot fastboot
```

Your Pocket DS will reboot into Fastboot mode.

**Step 2. Flash the Patched Image**

If your active slot was B, enter:

```
fastboot flash init_boot init_boot_b.img
```

If your active slot was A, enter:

```
fastboot flash init_boot init_boot_a.img
```

<img width="1373" height="150" alt="image" src="https://github.com/user-attachments/assets/4bc1b59a-3646-4e64-92e3-f47ed9805ba6" />


Wait until the flashing process finishes successfully.

**Step 3. Reboot Your Device**

Enter:

```
fastboot reboot
```

Your Pocket DS will reboot into Android.

Root access enabled!

Congratulations! Your AYANEO Pocket DS now has root access.





# **Part 6 – Unrooting (Restoring the Original Boot Image)**

If you want to remove root access and restore your Pocket DS to its original state, follow these instructions.

We will use the original boot images that we extracted and saved at the beginning of this guide.

The procedure is almost identical to the rooting process, except that we will flash the original image instead of the Magisk-patched image.

## **Step 1 – Open Platform Tools**

On your computer, open the folder where you extracted Android SDK Platform Tools.

Click the address bar, type:

```
cmd
```

Press Enter.

## **Step 2 – Check the ADB Connection**

Connect your Pocket DS to your computer with USB debugging enabled.

Enter:

```
adb devices
```

Make sure your device appears in the list.

## **Step 3 – Enter Fastboot Mode**

Enter:

```
adb reboot fastboot
```

Your Pocket DS will reboot into Fastboot mode.

## **Step 4 – Verify the Fastboot Connection**

Enter:

```
fastboot devices
```

Make sure your device is listed.

## **Step 5 – Identify the Active Slot**

Enter:

```
fastboot getvar current-slot
```

The command will tell you which slot is currently active.

For example:

```
current-slot: b
```

In this example, the active slot is B.

We must now restore the original `init_boot_b.img` file.

IMPORTANT – DO NOT MIX UP THE FILES!

Use the original boot image that you extracted from your device at the beginning of the rooting process.

Do NOT use the Magisk-patched image.

Also, remember that the active slot can change after an official system update.

Always check the active slot before flashing anything.

## **Step 6 – Prepare the Original Image**

Find the original boot image you saved earlier.

Depending on your active slot:

- Slot B: Use your original `init_boot_b.img`.
- Slot A: Use your original `init_boot_a.img`.

Copy the appropriate original image into your `platform-tools` folder.

Make sure the filename matches the active slot.

## **Step 7 – Restore the Original Boot Image**

If your active slot is B, enter:

```
fastboot flash init_boot init_boot_b.img
```

If your active slot is A, enter:

```
fastboot flash init_boot init_boot_a.img
```

Wait until the flashing process finishes successfully.

## **Step 8 – Reboot Your Device**

Enter:

```
fastboot reboot
```

Your Pocket DS will reboot into Android.

Original system restored!

Root access has now been removed, and your original boot image has been restored.

**A few important notes before publishing:**

1. Keep both original boot images in a safe place. Never overwrite your only backups with Magisk-patched images.
2. Always check the active slot before flashing.
3. The active slot may change after an official OTA system update.
4. This procedure modifies a critical boot image. Flashing the wrong image can prevent the device from booting.
