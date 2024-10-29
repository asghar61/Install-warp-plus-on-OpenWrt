# Install warp-plus on OpenWrt
# Router: pc x86/64
# OpenWrt Version: OpenWrt 23.05.5 r24106-10cc5fcd00  stable
# GitHub repo: https://github.com/asghar61/Install-warp-plus-on-OpenWrt
# ------------------------------------------
# ------------------------------------------

#install passwall & passwall 2  :https://github.com/amirhosseinchoghaei/Passwall
# ------------------------------------------

# 1. Install PassWall2 on OpenWrt (How? )
# ------------------------------------------

# 2- Install warp-plus

ssh root@192.168.27.1 #(Your Router's IP)
opkg update
opkg install openssh-sftp-server   ( do not conected sftp server)

# Download WARP PLUS based on your Router's CPU Architecture:x86/64

https://github.com/bepass-org/warp-plus/releases

# Extract the file and RENAME the binary file to > warp

# Transfer the file to the Router > /usr/bin (with tools like WinSCP, VSCode, ...)
# Make it executable:
chmod +x /usr/bin/warp

# Create System Service file for WARP:
vi /etc/init.d/warp
# Switch to Insert mode (Press i) & Paste this text block:
###

#!/bin/sh /etc/rc.common

START=91

USE_PROCD=1

PROG=/usr/bin/warp

start_service() {
  args=""
  args="$args -b 127.0.0.1:9090 --scan"
  procd_open_instance
  procd_set_param command $PROG $args
  procd_set_param stdout 1
  procd_set_param stderr 1
  procd_set_param respawn
  procd_close_instance
}

###
# Save & exit the editor (Esc > :x)

# Change the permissions of the file:
chmod 755 /etc/init.d/warp

#Enable the service:
service warp enable
#Start the service:
service warp start
#Check the service status:
service warp status

# Go to Luci-app (OpenWrt web) > Passwall2 and create a sockes config to:
127.0.0.1:9090
# Enable Main switch & Socks Config

--------------------------------------------
# Video Link:
--------------------------------------------


# injoy :)
# asghar
# youtube.com/@8bit-1bytee
