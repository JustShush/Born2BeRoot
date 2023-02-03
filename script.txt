#!/bin/bash

Arc="`uname -a`" #(ou -v)
CPU="cat /proc/cpuinfo | grep "physical id" | wc -l"
VCPU="cat /proc/cpuinfo | grep "processor" | wc -l"
Ram="`free --mega | awk '/Mem/{printf("%d/%dMB (%.2f%% usage)", $4, $2, $3/$2*100)}'`"
Mem="`df -H --total | awk '/total/ {printf("%d/%dGB (%.2f%% usage)", $4, $2, $3/$2*100)}'`"
Load="`top -bn1 | awk '/^top/ {printf("%.2f%%", $(NF-2))}'`"
Bootdate="`who -b | awk '{print $3" "$4}'`"
LVM=(`if [ "$(lsblk | grep lvm | wc -l)" -gt 0 ]; then printf "Yes"; else printf "No"; fi`)
TCP="`ss | grep tcp | wc -l` Established"
Logs="`who | cut -d ' ' -f 1 | sort -u | wc -l`"
Ip="`hostname -I`(`ip a | grep link/ether | awk '{print $2}'`)"
Sudo="cat /var/log/sudo/cmd.log | grep 'COMMAND' | wc -l"

wall "
	#Architecture: $Arc
	#CPU physical: $CPU
	#vCPU: $VCPU
	#RAM: $Ram
	#Disk Memory: $Mem
	#CPU load: $Load
	#Last boot: $Bootdate
	#LVM: $LVM
	#Connections TCP: $TCP
	#User log: $Logs
	#Network: IP $Ip
	#Sudo: $Sudo
"
