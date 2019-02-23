# refind-config
![screenshot](https://i.imgur.com/RBiP9oe.png)

this refind configuration is the darkened and modified version of the source i've forked. this repo doesn't exist for others to use as it's highly modified to suit my needs but feel free to take whatever as you please.

in a case where you feel like using my configuration, do not forget to modify the boot menu entries and hidden directories for it to match your system as i directly use the `refind.conf` as my theme config file instead of adding a `theme.conf` as an entry to `refind.conf`.

## modificiations i've done:
- modified directory names.
- removed the options for other icon sizes.
- removed the other font options leaving only the `adobe source code pro, 14px`.
- removed the old background and selection `.png`'s, replaced them with darkened ones.
- removed the `theme.conf`, merged it with my `refind.conf`.

## adding rEFInd to grub
```
menuentry "rEFInd bootloader"{
	insmod part_gpt
	insmod fat
	set root='hd0,gptX'
	if [ x$feature_platform_search_hint = xy ]; then
	  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gptX --hint-efi=hd0,gptX --hint-baremetal=ahci0,gptX  XXXX-XXXX
	else
	  search --no-floppy --fs-uuid --set=root XXXX-XXXX
	fi
	chainloader /EFI/refind/refind_x64.efi
}
```

- replace `hd0,gptX` with the correct `ESP` partition of you EFI.
⋅⋅⋅you can think of `hd0` as `sda` and `gptX` as `sdaX` so `hd0,gpt2` would be `/dev/sda2`.
- change the `XXXX-XXXX` with the `UUID` of your `ESP` partition.
⋅⋅⋅you can get the `UUID` of your `ESP` by running the `blkid` as root.
- you can change the `menuentry` line inside the quotation marks to change the display name of the entry.
