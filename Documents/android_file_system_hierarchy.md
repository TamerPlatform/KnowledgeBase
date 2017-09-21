# Android File System Hierarchy

This page will contain a replica structure of Android File System

/ : Base system

* ??? cache
    Cache Folder : Used as scratch pad by OS place dex optimized dalvik bitecode
* ??? data
    Contains USER Data Stored as a separate partition in mtdblocks mounted at bootup   
    * anr
    * idd
    * system
    * radio
    * property
    * ??? app
        Application : User installed
    * ??? data
        Downloaded, updated and manually installed apps folder for each app named as package name.
    * ??? local
* dalivk-cache
* ??? "default.prop"
    Default property settings, values restored from this file on every restart. Changes in this file will not be retained.
* ??? dev
    Device file system pointers
    * ??? "tty 1 - 63"
    * ??? null
    * ??? zero
    * ??? block
        Block Devices
        * ??? "loop 0-7"
            Loop back devices
        * ??? "mtdblock 0 - 6-8"
            MTD BLOCKS : Device internal memory
        * ??? mmcblk0
            SDCARD Block Device
* ??? "etc -> /system/etc"
    Soft link to /system/etc Directory
* hw_config.sh
* ??? init
    INIT executable, this is also the place where device nodes are created by listening to uevents
* ??? "init.rc"
    Initial Configuration file : decompressed from ramdisk
* ??? "logo.rle"
    Boot Time Logo
* ??? proc
    * ??? last_kmsg
        Previous Sessions Kernel message log
    * partitions
    * diskstats
    * ??? kmsg
        Kernel Message log simmilar to dmesg in linux
    * ??? cpuinfo
        CPU information simmillar to linux
    * ??? "config.gz"
        Copy of .config used to compile kernel (optional)
* ??? root
* ??? sbin
    Part of Ramdisk Content : This contains various executables required for Bootup
* ??? adbd
    ADB Daemon executable: Responsible for adb shell
* ??? sys
    * fs
    * devices
    * dev
    * bus
    * class
    * firmware
    * kernel
    * power
    * module
    * block
    * ??? Test
        Testing
* ??? system
    Main OS System: Stored as a separate partition in mtdblocks mounted at bootup (read-only)
    * ??? app
        System Apps : Pre installed : Android Specific, Vendor and Carrier Provided Application set. These applications can't be changed without rooting device(till version 4.0 of android)
    * ??? bin
        Binary Executables required for operation
    * ??? build.prop
        File containing Configuration variables used to define various operational parameters
    * ??? etc
        Configuration Files for Whole Android System
    * ??? framework
        Framework : jar Files which provision the interaction between applications and hardware
    * ??? fonts
        Fonts used in display
    * ??? media
        Contains Media files ringtone/alarms etc
    * ??? xbin
        Excutable Files generally this holds special executables like busybox or toolbox
* ??? sdcard
    SDCARD :removable sdcard directory
* ??? mnt
    * ??? sdcard -> /sdcard
        Link too /sdcard
    * ??? asec
        SDCARD Secure area


### Does this looks wrong

This is a work in progress Feel free to suggest changed either via issues / pull request @ github or sending email to androidfs@androidtamer.com


### Changelog
* 21 Sep 2017
    1. Data ported to github
* 11 Dec 2011
    1. Updated lots of data based on details from https://github.com/keesj/gomo/wiki/AndroidUserland and user comments
    1. Not just mouseover text is also available next to folders now.