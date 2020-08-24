# USBIP-How-to-make-it-work

OS Used - Manjaro Kernel 5.45.5_rt33-1

  -- Install -- Client and Server
sudo pacman -S usbip

  -- Prepwork -- Server Only, Where you plug USB devices into
  Usbip is broken and requires some love to get to work.
  Init. Drivers
sudo modprobe usbip-core
sudo modprobe usbip-host

  Getting a list of USB Devices. It's best to do now because things will get messy later.
  Remember what the bus id is looks like (. after may be optional): #-#.#
usbip --debug list -l

  Getting User Access to usb drivers (May be unsafe, I don't know)
sudo chown USER:GROUP -R /sys/bus/usb/drivers/usb/
sudo chmod 777 -R /sys/bus/usb/drivers/usb/
sudo chown USER:GROUP -R /sys/bus/usb/drivers/usbip-host/
sudo chmod 777 -R /sys/bus/usb/drivers/usbip-host/

  -- Binding USB Devices --
  Starting Daemon for connections to get handeled to. Port might be 3402 i think?
sudo usbipd -D
sudo usbip bind -busid=#-#.#
  
  --Client Side -- Other Machine
  See install instructions. :D
sudo modprobe usbip-core
sudo modprobe vhci-hcd
sudo usbip bind -r IPONLYOFSERVER -b #-#.#
