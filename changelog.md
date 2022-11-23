# Changelog

-------------------------------------------------------------------------------------

- 06/10/2022
	* Release with OC Mod 0.8.1, all kext are up to date

-------------------------------------------------------------------------------------
- 07/05/2022
	* Bump OC to 0.8.2 (Moded)
	* Fix DSDT issues (SMBUS, RTC, etc.)
	* Clean boot arg
	* Update kext
	* Use FakeSMC instead of VirtualSMC to make macOS detected battery better
	* Fixed boot loop with HDMI port
	* Fixed Power management
	* Add new feature: Enable TRIM without use terminal to force enable

-------------------------------------------------------------------------------------
- 11/10/2022 (0.8.6)
	* NEW DSDT: Rename EC0, BAT1 (this computer only have 1 battery), detele unused device.
	* For more stable while using hack, <a href="https://github.com/CloverHackyColor/FakeSMC3_with_plugins">FakeSMC3</a> now will use with this EFI.
	* Update kext to lastest version, Update OC to 0.8.6.
	* Add PCIe port to config.plist.
	* Change smbios to Macbook Pro.
	* Add new SSDT-PLUG and new power management kext (CPUFriend(Friend)). Now you can change smbios to newer version without lossing PM.
	* Remove unused patch and kext.
	* Fix HDMI output problems.
	* Add Inject EDID, now you can choose more resolution for your mac!
	* Fix double wake at lid when computer sleep.