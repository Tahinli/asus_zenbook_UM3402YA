# Asus Zenbook UM3402YA Linux Ses Sorunu Çözümü

## 6.8 KERNEL İLE BİRLİKTE BUNA İHTİYAÇ KALMADI, 6.8 VE DAHA ÜZERİ İÇİN HİÇBİR ŞEY YAPMANIZA GEREK YOK
> Detaylar:

> https://lore.kernel.org/all/1435594585.650325975.1707867511062.JavaMail.zimbra@free.fr/

> https://wiki.archlinux.org/title/ASUS_Zenbook_UM3402YA

## 6.8 VEYA ÜZERİ KERNEL KULLANAMIYORSANIZ AŞAĞIDAKİ ADIMLARLA YAMAYI UYGULAYABİLİRSİNİZ

* Kernel Sürümünüz 6.2 ve üzeri olmalı.
* Gerekirse ssdt-csc3551.dsl dosyası düzenlenebilir.
* Secure-Boot ayarını BIOS üzerinden kapatmayı gerektirebilir.

* Öncelikle dsl çıktısını derlemek için "acpica-tools" a ihtiyacımız var.

  APT kullanan dağıtımlar için: ```sudo apt install acpica-tools```
  
  DNF kullanan dağıtımlar için: ```sudo dnf install acpica-tools```

  PACMAN kullanan dağıtımlar için: ```sudo pacman -S acpica```
  
* Devamında dosyayı indirdiğiniz klasöre gidip aşağıdaki kodu çalıştırın.
* Bu kod dsl dosyamızı aml uzantılı dosyaya derleyecektir.
  
  ```iasl -tc ssdt-csc3551.dsl```

* Elde ettiğimiz dosyayı /boot dizinine kopyalayın

  ```sudo cp -f ssdt-csc3551.aml /boot```
* Elde ettiğimiz dosyayı bilgisayar açılırken sistemimize tanıtmak için sistem başlatıcımıza -grub- "acpi" dosyamızı kopyalıyoruz.
* Aşağıdaki komut ile bunu yapabilirsiniz.
  
  ```sudo cp -f 01_acpi /etc/grub.d```
* Attığımız acpi dosyasının çalışması için onu çalıştırılabilir hale getiriyoruz.
  
  ```sudo chmod +x /etc/grub.d/01_acpi```

* En son yaptığımız değişiklilerden "grub" dostumuzu haberdar etmek için güncelliyoruz.

  ```sudo update-grub```
* Ubuntu temelli olmayan sistemlerde ```update-grub``` olmayabilir onun yerine aşağıdakini kullanabilirsiniz.
* Fedora / RHEL temelli dağıtımlar için ( teşekkürler @effepi0 )

    ```sudo grub2-mkconfig -o /etc/grub2.cfg```

    ```sudo grub2-mkconfig -o /etc/grub2-efi.cfg```

* Arch temelli dağıtımlar için ( teşekkürler @kelna )

    ```grub-mkconfig -o /boot/grub/grub.cfg``` (sudo yetkisi gerekebilir)

### Kaynakça
* https://github.com/farfaaa/asus_zenbook_UM3402YA -Original Repo- (Really Appreciate My Friend, Thanks a Lot)
* https://wiki.archlinux.org/title/ASUS_Zenbook_UM3402YA
* https://gist.github.com/lamperez/d5b385bc0c0c04928211e297a69f32d7
* https://gist.github.com/lamperez/862763881c0e1c812392b5574727f6ff
* https://gist.github.com/masselstine/8fe9634b4c31cef07b8dfab089e4eb38
* https://github.com/thor2002ro/asus_zenbook_ux3402za (UX3402ZA dst dosyası için bu arkadaşa bakabilirsiniz, adımlar aynı şekilde uygulanabilir)
