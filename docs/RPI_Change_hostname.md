# How to change the Hostname of Raspberry PI

> Run the following commands to change the hostname from **raspberrypi** to  __**raspberrypi2**__
This will update and restart the pi to update the name of pi

```bash
sudo sed -i 's/\<raspberrypi\>/raspberrypi2/g' /etc/hostname
sudo sed -i 's/\<raspberrypi\>/raspberrypi2/g' /etc/hosts
sudo shutdown -r now
```

## Reference: 
<https://thepihut.com/blogs/raspberry-pi-tutorials/19668676-renaming-your-raspberry-pi-the-hostname>
