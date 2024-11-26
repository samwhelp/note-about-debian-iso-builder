

# 首頁

> Debian / ISO Builder / 探索筆記

| Link | GitHub |
| ---- | ------ |
| [ISO Builder 探索筆記](https://samwhelp.github.io/note-about-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-iso-builder) |
| [Debian / ISO Builder / 探索筆記](https://samwhelp.github.io/note-about-debian-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-debian-iso-builder) |




## 主題

* [實作案例](#實作案例)
* [Boot ISO By GRUB](#boot-iso-by-grub)
* [Debian OS / Live System](#debian-os--live-system)
* [相關筆記](#相關筆記)




## 實作案例

| 實作案例 |
| ------- |
| [debian-iso-builder-start](https://github.com/samwhelp/debian-iso-builder-start) |




## Boot ISO By GRUB

> 將產出的「iso檔案」放置到「`/opt/iso/debian/latest/debian.iso`」這個路徑

> 產生一個檔案「`/boot/grub/custom.cfg`」，內容如下

``` sh
menuentry "Lika OS" --class Debian {
	set iso_file="/opt/iso/debian/latest/debian.iso"
	search --set=iso_partition --no-floppy --file $iso_file
	probe --set=iso_partition_uuid --fs-uuid $iso_partition
	set img_dev="/dev/disk/by-uuid/$iso_partition_uuid"
	loopback loop ($iso_partition)$iso_file

	set extra_option=""
	#set extra_option="components quiet splash"

	set locale_option=""
	#set locale_option="locales=en_US.UTF-8"
	#set locale_option="locales=zh_TW.UTF-8"
	#set locale_option="locales=zh_CN.UTF-8"
	#set locale_option="locales=zh_HK.UTF-8"
	#set locale_option="locales=ja_JP.UTF-8"
	#set locale_option="locales=ko_KR.UTF-8"

	set boot_option="${locale_option} ${extra_option}"
	linux	(loop)/live/vmlinuz boot=live buuid=${iso_partition_uuid} findiso=${iso_file} ${boot_option}
	initrd	(loop)/live/initrd.img
}
```

> 重新開機後，就會在「GRUB」的開機選單，看到「`Lika OS`」這個選項。




## Debian OS / Live System

| Account  | Value  |
| -------- | ------ |
| Username | `user` |
| Password | `live` |

若想要移除目前帳號的密碼，可以執行下面指令

``` sh
sudo passwd -d $(whoami)
```




## 相關筆記

| Link | GitHub |
| ---- | ------ |
| [Debian 探索筆記](https://samwhelp.github.io/note-about-debian/) | [GitHub](https://github.com/samwhelp/note-about-debian) |
| [Eznixos 探索筆記](https://samwhelp.github.io/note-about-eznixos/) | [GitHub](https://github.com/samwhelp/note-about-eznixos) |
| [Lika OS 探索筆記](https://samwhelp.github.io/note-about-lika/) | [GitHub](https://github.com/samwhelp/note-about-lika) |
| [Lika OS / Live Build Config / 探索筆記](https://samwhelp.github.io/note-about-lika-live-build-config/) | [GitHub](https://github.com/samwhelp/note-about-lika-live-build-config) |





## Samwhelp

* [個人筆記](https://samwhelp.github.io/book/)
