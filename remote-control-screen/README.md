# Using Android/PC as a Second Monitor in Linux

(Using Android/PC as a Second Monitor in Linux)[https://sangams.com.np/using-android-pc-as-a-second-monitor-in-linux/]

## Install x11vnc

~~~ bash
sudo pacman -Syu x11vnc
~~~

## Available displays and outputs ports

~~~ bash
xrandr
~~~

## Create a new mode for the secondary monitor

~~~ bash
gtf 1920 1200 60

gtf 1920 1200 30
~~~

will return:
~~~
# 1920x1200 @ 60.00 Hz (GTF) hsync: 74.52 kHz; pclk: 193.16 MHz
  Modeline "1920x1200_60.00"  193.16  1920 2048 2256 2592  1200 1201 1204 1242  -HSync +Vsync

# 1920x1200 @ 30.00 Hz (GTF) hsync: 36.63 kHz; pclk: 89.67 MHz
  Modeline "1920x1200_30.00"  89.67  1920 1992 2184 2448  1200 1201 1204 1221  -HSync +Vsync
~~~

## Add a new mode for our Android device

rewrite line 'Modeline' from above as '--newmode' below 

~~~ bash
xrandr --newmode "1920x1200_60.00" 193.16  1920 2048 2256 2592  1200 1201 1204 1242  -HSync +Vsync

xrandr --newmode "1920x1200_30.00" 89.67  1920 1992 2184 2448  1200 1201 1204 1221  -HSync +Vsync
~~~

## Add this new mode to the unused display: HDMI1

value 'HDMI1' taken from output of xrandr

~~~ bash
xrandr --addmode HDMI1 1920x1200_60.00
~~~

## Enable HDMI1 and place it next to eDP1

[--left-of output] [--right-of output] [--above output] [--below output] 

~~~ bash
xrandr --output HDMI1 --mode 1920x1200_60.00 --below HDMI2


xrandr --output VIRTUAL1 --mode 1920x1200_60.00 --below HDMI2 --scale 1.0x1.0
~~~


## Start VNC server and only allow to show the right portion of the screen which can’t be seen in default display

<width>x<height>+<offset_x>+<offset_y>

~~~ bash
x11vnc -clip 1920x1200+0+0
~~~


## exit xrandr

~~~ bash
xrandr --output HDMI1 --off 
~~~




## Installation

https://sangams.com.np/using-android-pc-as-a-second-monitor-in-linux/

https://linuxconfig.org/how-to-share-your-desktop-in-linux-using-x11vnc

https://xorg-team.pages.debian.net/xorg/howto/use-xrandr.html

### Linux

#### 1. Install VNC server (x11vnc) 
~~~
sudo pacman -Syu x11vnc
~~~

#### 2. Configure firewall (ufw)
~~~
sudo ufw allow 5900/tcp
~~~

#### 3. Show available displays
~~~
xrandr
~~~

#### 4. Creating a new mode for the new monitor
~~~
gtf 960 540 30
gtf 1920 1080 60
~~~

Which gives VESA GTF mode lines for 1280×720 @ 60 fps. This results;
~~~
# 1920x1080 @ 60.00 Hz (GTF) hsync: 67.08 kHz; pclk: 172.80 MHz
Modeline "1920x1080_60.00"  172.80  1920 2040 2248 2576  1080 1081 1084 1118  -HSync +Vsync

# 960x540 @ 30.00 Hz (GTF) hsync: 16.50 kHz; pclk: 17.95 MHz
Modeline "960x540_30.00"  17.95  960 936 1024 1088  540 541 544 550  -HSync +Vsync
~~~

#### 5. Adding a new mode for our Android device
~~~
xrandr --newmode "1920x1080_60.00"  172.80  1920 2040 2248 2576  1080 1081 1084 1118  -HSync +Vsync

xrandr --newmode "960x540_30.00"  17.95  960 936 1024 1088  540 541 544 550  -HSync +Vsync
~~~

#### 6. Adding the new mode to the unused display (VIRTUAL1)
~~~
xrandr --addmode VIRTUAL1 1920x1080_60.00

xrandr --addmode VIRTUAL1 960x540_30.00
~~~

#### 7. Enabling VIRTUAL1 and moving it (--right-of/--left-of/--above/--below)
~~~
xrandr --output VIRTUAL1 --mode 1920x1080_60.00 --below HDMI2

xrandr --output VIRTUAL1 --mode 960x540_30.00 --below HDMI2
~~~

#### 8. Run VNC server
~~~
x11vnc -viewonly -clip 1920x1080+0+2160

x11vnc -viewonly -clip 960x540+0+2160

x11vnc -viewonly -display :0 -passwd secretPassword -clip 1920x1080+0+2160
~~~
~~~
-clip WxH+X+Y          Only show the sub-region of the full display that
                       corresponds to the rectangle geometry with size WxH and
                       offset +X+Y.  The VNC display has size WxH (i.e. smaller
                       than the full display).  This also works for -id/-sid
                       mode where the offset is relative to the upper left
                       corner of the selected window.  An example use of this
                       option would be to split a large (e.g. Xinerama) display
                       into two parts to be accessed via separate viewers by
                       running a separate x11vnc on each part.
~~~

#### 9. Check ip and connect
~~~
ip a
~~~

#### 10. Deleting mode
~~~
xrandr --delmode VIRTUAL1 1920x1080+0+2160

xrandr --delmode VIRTUAL1 960x540_30.00
~~~


### Android

#### Install vnc client - multivnc





