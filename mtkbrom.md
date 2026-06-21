# MTK BROM/BROM Handshake

## The MediaTek (MTK) BootROM handshake is the initial communication protocol that allows external software to talk directly to a device’s unalterable, hardware-level BootROM. 

### It serves as a rescue or development pathway used to unbrick, root, or extract data from a device when it cannot boot into normal operating mode. Sometimes, some people also use it to do things such as changing IMEI, S/N, exploiting the TEE (Trusted Execution Environment) & more

***

## How the Handshake Works

### Setting up - old devices

#### When a MediaTek-powered device is completely turned off and connected via USB, its CPU briefly exposes a hardware-level COM port for about 1 second before booting into standard charging mode. 

***

### Setting up - Newer devices/prior to One UI 7

#### You can use the test-points, GPIOs that are often named as "KCOL0", "KROW0", "TP". Most Samsung devices' test-points are not named on the motherboard.

***

### Setting up - Newer devices/One UI 7+ (such a shame)

#### It seems like only several bricking issues would lead to the handshake nowadays, however you can find more info about it in the main README

***

#### The handshake intercepts this brief window:
The Request (SYNC): 

   ```- The computer sends a specific 4-byte hexadecimal sequence (e.g., A0 0A 50 05) to the device's BootROM.```

The Response (ACK): 

   ```- The device’s hardware acknowledges the signal by replying with the bitwise inverse of those bytes (e.g., 5F F5 AF FA).```

The Session: 

   ```- Once both sides confirm the transmission, a secure low-level connection is established.```

   ```- This allows the computer to send a "Download Agent" (DA) payload to flash, back up, or manipulate the device’s internal partitions.```

***

### When and Why It Is Used

##### Unbricking Devices: 

- If a bad software update causes a phone or router to go into a boot loop, the BootROM handshake can force-flash stock firmware back onto the device without needing standard bootloader access.

##### Bootloader Unlocking & Rooting: 

- Modding tools (like [mtkclient](https://github.com/bkerler/mtkclient)) from [bkerler](https://github.com/bkerler)) use the handshake to overwrite security partitions, bypass lock states, or temporarily disable BootROM protections to unlock the bootloader.

- Forensic Data Extraction: Because the BootROM is hardware-baked, forensic software relies on this handshake to pull raw memory dumps from the device, even when the OS is locked or heavily encrypted.
