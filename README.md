surfacepro3-bijju
=================

Surface Pro 3 Kernel for Fedora 20 or Korora 20
Got the Keyboard and touch pad working as well (well thank internet search engine not me): 

1. Downloaded New Kernel from kernel.org (3.16.2) updated 2 files 
  a) Linux-3.16.2xxxxx/drivers/hid/hid-ids.h b/drivers/hid/hid-ids.h and added below statement at line 637 
      define USB_DEVICE_ID_MS_TYPE_COVER_3 0x07dc 
  b) Linux-3.16.2xxxxx/drivers/hid/hid-ids.h b/drivers/hid/hid-microsoft.c and added below statement at line 274 
      { HID_USB_DEVICE(USB_VENDOR_ID_MICROSOFT, USB_DEVICE_ID_MS_TYPE_COVER_3), 
          .driver_data = 0 }, 
  c) Recompiled the kernel and generated rpm files and installed new rpm files generated 
     (N0te: install necessary packages if prompted)
      make -j `getconf _NPROCESSORS_ONLN` rpm-pkg LOCALVERSION=-surfacepro3-bijju

2. Create a xorg.conf with below content, move the xrog.conf to /etc/X11/ and reboot 
      Section "InputClass" 
        Identifier "Surface Pro 3 cover" 
        MatchIsPointer "on" 
        MatchDevicePath "/dev/input/event*" 
        Driver "evdev" 
        Option "vendor" "045e" 
        Option "product" "07dc" 
        Option "IgnoreAbsoluteAxes" "True" 
      EndSection

What Works: 
  1. Dual Monitor with mini-Display port [Good]
  2. Keyboard [Good]
  3. Touch Pad [Good]
  4. Battery Somewhat [maybe 5-6 hrs, tweaking setting will probably yield better performance like brightness, powertop, etc.....]
  5. USB ports work good
  6. Bluetooth and Wifi Works need to get the Firmware and reboot 
        git clone git://git.marvell.com/mwifiex-firmware.git 
        su -c "cp mwifiex-firmware/mrvl/* /lib/firmware/mrvl/"
  7. Micro SD Card Reader 
     for exFAT sdcards to work install 
        su -c "yum install exfat-utils fuse-exfat"


What is NOT Working
  1. Camera (both Front and Rear)
  2. Volume Buttons
  3. NOT SURE WHAT ELSE I missed

Questions: ?
