# SVF14217SGW Hackintosh

![lspcon_debug](./img/desktop.png)

## Attention: Please read all the issues I wrote here before you use this EFI!
May you will asked why should you read all of the issues here. The answer is:
- The VAIO notebooks series are the hardest notebook to Hackintosh. The main reason is it didn't support 'Boot Priority' in UEFI!
- Required DSDT to patch to make some hardware working, not SSDT (except: GPU, etc.)

* Issues:
<details>
	<summary>Dual Booting</summary>
	For some reason, almost VAIO notebooks come from 2016 or older (I donn't sure about that!) didn't have any option in UEFI called: 'Boot Priority'. So, that mean there're many challenge come with that. To fixed this, we inly have 1 solution: Using EasyUEFI to custom boot entry! Download <a href="https://www.easyuefi.com/index-us.html">EasyUEFI</a>
	To add OpenCore and make it boot first instead of Windows Boot Manager (WBM). Please choose OpenCore.efi from /EFI/OC/OpenCore.efi. For full guide, please read <a href="https://www.olarila.com/topic/13072-dual-boot-guide-clover-and-open-core/">here.</a>
</details>
