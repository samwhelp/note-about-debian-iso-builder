

# 首頁

> Debian / ISO Builder / 探索筆記

| Link | GitHub |
| ---- | ------ |
| [ISO Builder 探索筆記](https://samwhelp.github.io/note-about-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-iso-builder) |
| [Debian / ISO Builder / 探索筆記](https://samwhelp.github.io/note-about-debian-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-debian-iso-builder) |
| [Ubuntu / ISO Builder / 探索筆記](https://samwhelp.github.io/note-about-ubuntu-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-ubuntu-iso-builder) |
| [debian-iso-builder-maintain](https://samwhelp.github.io/debian-iso-builder-maintain/) | [GitHub](https://github.com/samwhelp/debian-iso-builder-maintain) |




## 主題

* [Docker](#docker)
* [ISO Builder Template](#iso-builder-template)
* [Respin](#respin)
* [Boot ISO By GRUB](#boot-iso-by-grub)
* [Live Account](#live-account)
* [相關案例](#相關案例)
* [相關筆記](#相關筆記)




## Docker

| Docker Image |
| ------------ |
| [distro-iso-builder-docker-image](https://github.com/samwhelp/distro-iso-builder-docker-image) |
| [debian-docker-image](https://github.com/samwhelp/debian-docker-image) |




## ISO Builder Template

| Link | GitHub |
| ---- | ------ |
| [debian-live-custom-template](https://samwhelp.github.io/debian-live-custom-template/) | [GitHub](https://github.com/samwhelp/debian-live-custom-template) |
| [debian-live-create-template](https://samwhelp.github.io/debian-live-create-template/) | [GitHub](https://github.com/samwhelp/debian-live-create-template) |
| [debian-iso-builder-template](https://samwhelp.github.io/debian-iso-builder-template/) | [GitHub](https://github.com/samwhelp/debian-iso-builder-template) |




## Respin

> [更多...](https://samwhelp.github.io/note-about-debian-iso-builder/read/respin.html)

| Remix | Respin |
| ----- | ------ |
| [debian-iso-builder-remix-gnome-shell](https://github.com/samwhelp/debian-iso-builder-remix-gnome-shell) | [debian-iso-builder-respin-gnome-shell](https://github.com/samwhelp/debian-iso-builder-respin-gnome-shell) |
| [debian-iso-builder-remix-kde-plasma](https://github.com/samwhelp/debian-iso-builder-remix-kde-plasma) | [debian-iso-builder-respin-kde-plasma](https://github.com/samwhelp/debian-iso-builder-respin-kde-plasma) |
| [debian-iso-builder-remix-xfce](https://github.com/samwhelp/debian-iso-builder-remix-xfce) | [debian-iso-builder-respin-xfce](https://github.com/samwhelp/debian-iso-builder-respin-xfce) |
| [debian-iso-builder-remix-lxqt](https://github.com/samwhelp/debian-iso-builder-remix-lxqt) | [debian-iso-builder-respin-lxqt](https://github.com/samwhelp/debian-iso-builder-respin-lxqt) |
| [debian-iso-builder-remix-mate](https://github.com/samwhelp/debian-iso-builder-remix-mate) | [debian-iso-builder-respin-mate](https://github.com/samwhelp/debian-iso-builder-respin-mate) |
| [debian-iso-builder-remix-cinnamon](https://github.com/samwhelp/debian-iso-builder-remix-cinnamon) | [debian-iso-builder-respin-cinnamon](https://github.com/samwhelp/debian-iso-builder-respin-cinnamon) |
| [debian-iso-builder-remix-budgie](https://github.com/samwhelp/debian-iso-builder-remix-budgie) | [debian-iso-builder-respin-budgie](https://github.com/samwhelp/debian-iso-builder-respin-budgie) |


| Remix | Respin |
| ----- | ------ |
| [debian-iso-builder-remix-lxqt-with-kwin](https://github.com/samwhelp/debian-iso-builder-remix-lxqt-with-kwin) | [debian-iso-builder-respin-lxqt-with-kwin](https://github.com/samwhelp/debian-iso-builder-respin-lxqt-with-kwin) |
| [debian-iso-builder-remix-mate-with-compiz](https://github.com/samwhelp/debian-iso-builder-remix-mate-with-compiz) | [debian-iso-builder-respin-mate-with-compiz](https://github.com/samwhelp/debian-iso-builder-respin-mate-with-compiz) |




## Boot ISO By GRUB

> 將產出的「iso檔案」放置到「`/opt/iso/debian/latest/debian.iso`」這個路徑

> 產生一個檔案「`/boot/grub/custom.cfg`」，內容如下

``` sh
menuentry "Debian Live ISO" --class Debian {
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
	linux (loop)/live/vmlinuz boot=live buuid=${iso_partition_uuid} findiso=${iso_file} ${boot_option}
	initrd (loop)/live/initrd.img
}
```

> 重新開機後，就會在「GRUB」的開機選單，看到「`Debian Live ISO`」這個選項。


> [https://salsa.debian.org/live-team/live-boot](https://salsa.debian.org/live-team/live-boot)

> [https://salsa.debian.org/live-team/live-config](https://salsa.debian.org/live-team/live-config)




## Live Account

| Account  | Value  |
| -------- | ------ |
| Username | `live` |
| Password | `live` |


若想要更改目前帳號的密碼，可以執行下面指令

``` sh
sudo passwd $(whoami)
```


若想要移除目前帳號的密碼，可以執行下面指令

``` sh
sudo passwd -d $(whoami)
```




## 相關案例

| 相關案例 |
| ------- |
| [debian-iso-builder-start](https://github.com/samwhelp/debian-iso-builder-start) |




## 相關筆記

| Link | GitHub |
| ---- | ------ |
| [Debian 探索筆記](https://samwhelp.github.io/note-about-debian/) | [GitHub](https://github.com/samwhelp/note-about-debian) |
| [Ubuntu 探索筆記](https://samwhelp.github.io/note-about-ubuntu/) | [GitHub](https://github.com/samwhelp/note-about-ubuntu) |
| [Ubuntu / ISO Builder / 探索筆記](https://samwhelp.github.io/note-about-ubuntu-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-ubuntu-iso-builder) |


| Link | GitHub |
| ---- | ------ |
| [Eznixos 探索筆記](https://samwhelp.github.io/note-about-eznixos/) | [GitHub](https://github.com/samwhelp/note-about-eznixos) |
| [Lika OS 探索筆記](https://samwhelp.github.io/note-about-lika/) | [GitHub](https://github.com/samwhelp/note-about-lika) |
| [Lika OS / Live Build Config / 探索筆記](https://samwhelp.github.io/note-about-lika-live-build-config/) | [GitHub](https://github.com/samwhelp/note-about-lika-live-build-config) |




## Samwhelp

* [個人筆記](https://samwhelp.github.io/book/)
