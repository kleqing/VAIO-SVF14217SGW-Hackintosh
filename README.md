<h1 align="center">Sony VAIO SVF14217SGW Hackintosh</h1> 

![lspcon_debug](./img/desktop.png)
<h6 align="center">Desktop preview</h6>

## Attention: Please read all the issues I wrote here before you use this EFI!

May be you will asked me why should you read all of the issues here. The answer is:
- The VAIO notebooks series are the hardest notebook to Hackintosh. The main reason is it didn't support select "Boot Priority" in UEFI!
- Required DSDT to patch to make some hardware working, not SSDT (except: GPU, etc.)

* Issues:
	<details>
		<summary>Dual Booting</summary>
		<br>
		For some reason, almost VAIO notebooks come from 2016 or older (I donn't sure about that!) didn't have any option in UEFI called: 'Boot Priority'. So, that mean there're many challenge come with that. To fixed this, we inly have 1 solution: Using EasyUEFI to custom boot entry! Download <a href="https://www.easyuefi.com/index-us.html">EasyUEFI</a>
		<br>
		<br>
		To add OpenCore and make it boot first instead of Windows Boot Manager (WBM). Please choose OpenCore.efi from /EFI/OC/OpenCore.efi 
		<br>
		For full guide about this, please read <a href="https://www.olarila.com/topic/13072-dual-boot-guide-clover-and-open-core/">here</a>
	</details>

	<details>
		<summary>OpenCore inject DSDT and BDOS issue on Windows</summary>
		<br>
		As you now, OpenCore is my favourite bootloader because it supported more OSes and faster than Chameleon (Legacy) and Clover!
		<br>
		Beside, there're also many error come with this bootloader. Like using DSDT instead SSDT. The main reason for this is there are lot of various kext support more hardware. That mean you needn't use DSDT anymore, only use SSDT and hot-patch. But the VAIO notebooks aren't! They required DDST to make macOS read their battery! (Basically, <a href="https://github.com/1Revenger1/ECEnabler">ECEnabler</a> didn't work with some VAIO notebooks, they need DSDT to read the battery). And that mean OpenCore will inject our patched DSDT to all OSes and it cause BDOS on Windows! 
		<br>
		Luckily, Olarila have make a version to make OpenCore didn't inject patched DSDT to all OSes. You can check this: <a href="https://github.com/OlarilaHackintosh/OpenCore_NO_ACPI">OpenCore_No_ACPI</a>
		<br>
		<br>
		For more information about inject ACPI inject, you can read <a href="https://dortania.github.io/OpenCore-Install-Guide/why-oc.html#does-opencore-always-inject-smbios-and-acpi-data-into-other-oses">here</a>
	</details>

	<details>
		<summary>dGPU and NVIDIA Optimus</summary>
		<br>
		This is the true of pain on the VAIO notebook. As you now, Apple has removed NVIDIA Web Driver since macOS Mojave (10.14). That mean you can use Web Driver on 10.13.6 or older. Although you can turn off dGPU via UEFI, but as a gammer (i.e Genshin player) i cann't do that. Becasue if i want to go to Windows to play games, i have to go to UEFI and turn dGPU on, and when i want to use macOS, i have to repeat the action again. Seems like it will cost a lot of time! Dortania has showed a guide that turn dGPU off, you can read <a href="https://dortania.github.io/OpenCore-Install-Guide/extras/spoof.html#windows-gpu-selection">here</a> 
		<br>
		<br>
		Unfortunately, all VAIO notebooks doesn't have any option call NVIDIA Optimus! That mean you only have 2 options:
			<br> 
			1. Disable dGPU via UEFI
			<br> 
			2. Turn dGPU to s4 state (I use this method with disable dGPU via Device Properties to make my battery didn't drain too much)
		<br>
		<br>
		I recommend using option 1. But if you're a gammer, option 2 is the best choice!
	</details>

## Overview

- These specs I showed to you here are not original, some hardware was changed or replaced!

<details>
<summary>System Specs</summary>
	|  Name  | More infomation |
	| --------- | -------------------------- |
	| CPU | Intel Core i3 3227U 1.90 GHz |
	| GPU | Intel HD Graphics 4000 |
	| VGA | NVIDIA GeForce GT 740M |
	| Memory | 1333MHz DDR3 2x4GB |
	| Audio | Realtek ALC 233 |
	| Ethernet | Realtek RTL 8111 |
	| Wifi | BCM94352HMB |
	| Hard Disk Drive | Netac SSD 256GB|
	| Second Disk Drive | HGST 500GB |
</details>

- macOS Supported
 	| macOS | Status |
	| ------------- | ------------- | 
	| 10.14 | ✅ | 
	| 10.15 | ✅ | 
	| 11.0 | ✅ |
	| 12.0 | Untested |  

- Bootloader: OpenCore 0.8.1 Mod (<a href="https://github.com/OlarilaHackintosh/OpenCore_NO_ACPI">OpenCore_No_ACPI</a>)

- 💾 UEFI Config
	* Secure Boot: Disable (I've tried changed key but it will make break the system bootloader)
	* Boot mode: UEFI
	* 1st boot priority: External Device
	* External boot device: Enable
	* Wake on LAN: Unsupported

- Current Status
	| Feature | Status | Note |
	| ------------- | ------------- | ------------- | 
	| CPU | ✅ | |
	| GPU | ✅ | |
	| VGA | ❌ | Can get it turn to s4 state or turn off in UEFI |
	| Fn Key | ✅ | Requied patching DSDT for brightness key |
	| Brightness | ✅ | |
	| USB Port | ✅ | Recommend mapping in macOS using USBToolBox |
	| Audio | ✅ | Add `alcid=27` to boot-arg |
	| Battery | ✅ | Requied patching DSDT |
	| TouchPad | ✅ | Some time it cause reboot at boot |
	| Build-in Microphone | ✅ | |
	| Headphone & Speaker | ✅ | |
	| Camera | ✅ | |
	| Wifi & Bluetooth | ✅ | Need to replace |
	| Airdrop & Handoff | ✅ | Required wifi card support bluetooth 4.0 |
	| iMessage, Facetime & AppStore | ✅| |
	| Sleep | ✅ | Lid close get delay to sleep |
	| HDMI |  ✅ | HDMI Audio are working to! |
	| SD Card | ❌ | Can turn off by using SSDT to save battery |
	| WWAN | ❌ | |
	| FileVault | ⚠ | Untested |
<details>
<summary>Example: Configure the smoother for a Haswell-based laptop with Intel HD Graphics 4600</summary>

The following kernel logs are dumped from a Haswell laptop when a user changes the brightness from the lowest level to the highest one.  
Since the distance to the next level is relatively short, we use `N = 25` and `T = 8` instead,  
making the graphics driver transition to the next brightness level in approximately 200 milliseconds.

|     Device Property Name     | Type |   Value  |            Notes           |
|:----------------------------:|:----:|:--------:|:--------------------------:|
|   enable-backlight-smoother  | Data | 01000000 |     Enable the smoother    |
|   backlight-smoother-steps   | Data | 19000000 | 25 (0x19) in little endian |
|  backlight-smoother-interval | Data | 08000000 | 08 (0x08) in little endian |
| backlight-smoother-threshold | Data | 00000000 | 00 (0x00) in little endian |

```
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000000; Target = 0x00000036; Distance = 0054; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000036; Target = 0x00000036; Distance = 0000; Steps = 25; Stride = 0.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000036; Target = 0x00000054; Distance = 0030; Steps = 25; Stride = 2.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000054; Target = 0x0000007d; Distance = 0041; Steps = 25; Stride = 2.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x0000007d; Target = 0x000000b2; Distance = 0053; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000000b2; Target = 0x000000e7; Distance = 0053; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000000e7; Target = 0x000000f5; Distance = 0014; Steps = 25; Stride = 1.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000000f5; Target = 0x00000137; Distance = 0066; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000137; Target = 0x00000149; Distance = 0018; Steps = 25; Stride = 1.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000149; Target = 0x000001b1; Distance = 0104; Steps = 25; Stride = 5.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000001b1; Target = 0x0000022b; Distance = 0122; Steps = 25; Stride = 5.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x0000022b; Target = 0x00000271; Distance = 0070; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000271; Target = 0x000002b8; Distance = 0071; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000002b8; Target = 0x00000359; Distance = 0161; Steps = 25; Stride = 7.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000359; Target = 0x000003a4; Distance = 0075; Steps = 25; Stride = 3.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000003a4; Target = 0x00000401; Distance = 0093; Steps = 25; Stride = 4.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000401; Target = 0x00000413; Distance = 0018; Steps = 25; Stride = 1.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000413; Target = 0x0000046b; Distance = 0088; Steps = 25; Stride = 4.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x0000046b; Target = 0x000004ec; Distance = 0129; Steps = 25; Stride = 6.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000004ec; Target = 0x00000588; Distance = 0156; Steps = 25; Stride = 7.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000588; Target = 0x000005f3; Distance = 0107; Steps = 25; Stride = 5.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000005f3; Target = 0x000006b1; Distance = 0190; Steps = 25; Stride = 8.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000006b1; Target = 0x00000734; Distance = 0131; Steps = 25; Stride = 6.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000734; Target = 0x00000815; Distance = 0225; Steps = 25; Stride = 9.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x00000815; Target = 0x000008af; Distance = 0154; Steps = 25; Stride = 7.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000008af; Target = 0x000009f7; Distance = 0328; Steps = 25; Stride = 14.
igfx: @ (DBG) BLS: [COMM] Processing the request: Current = 0x000009f7; Target = 0x00000ad9; Distance = 0226; Steps = 25; Stride = 10.
```

As you can observe from the above log, the register value is `0x00` when the display is at the lowest brightness level.
When the user presses a key to increase the brightness, the register value becomes `0x36`, 
so in this case you may use a lowerbound, for example `0x18`, to prevent the display turning black.
You may want to analyze the kernel log produced by the DEBUG version to find a lowerbound that best works for your laptop.

</details>




