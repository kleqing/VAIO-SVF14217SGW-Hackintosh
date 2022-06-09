<h1 align="center">Sony VAIO SVF14217SGW Hackintosh</h1> 

![lspcon_debug](./img/desktop.png)
<h5 algin="center">Preview</h5>

## Attention: Please read all the issues I wrote here before you use this EFI!

May be you will asked me why should you read all of the issues here. The answer is:
- The VAIO notebooks series are the hardest notebook to Hackintosh. The main reason is it didn't support 'Boot Priority' in UEFI!
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

To make READEME.md clean, i will hide my laptop specs. But if you want to see my specs, you can expand "Specs" 

- Specs
	| Feature | Status |
	| ------------- | ------------- |
	| CPU | Intel(R) Core(TM) i3 3227U 1.9GHz |
	| GPU | Intel(R) HD Graphics 4000 |
	| VGA | NVIDIA GeForce GT 740M |
	| Memory | 1333MHz DDR3 2x4GB |
	| Audio | Realtek ALC 233 |
	| Ethernet | Realtek RTL 8111 |
	| Wifi | BCM94352HMB |
	| Hard Disk Drive | Netac SSD 256GB|
	| Second Disk Drive | HGST 500GB |

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
	| VGA | ❌ | Make it go to s4 or turn off in UEFI |
	| Fn Key | ✅ | Requied patching DSDT for brightness key |
	| Brightness | ✅ | |
	| USB Port | ✅ | Recommend mapping in macOS using USBToolBox |
	| Audio | ✅ | Add alcid=27 to boot-arg |
	| Battery | ✅ | Requied patching DSDT |
	| TouchPad | ✅ | Some time it cause reboot at boot |
	| Build-in Microphone | ✅ | |
	| Headphone & Speaker | ✅ | |
	| Camera | ✅ | |
	| Wifi & Bluetooth | ✅ | Need to replace |
	| Airdrop & Handoff | ✅ | Required wifi card support bluetooth 4.0 |
	| iMessage, Facetime & AppStore | ✅| |
	| Sleep | ✅ | Lid close have delay to sleep |
	| HDMI |  ✅ | HDMI Audio are working to! |
	| SD Card | ❌ | Can turn off using SSDT to save battery |
	| WWAN | ❌ | |
	| FileVault | ⚠ | Untested |





