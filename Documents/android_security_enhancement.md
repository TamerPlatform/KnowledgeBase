hide_toc: true

# Android Security Enhancement List

This page catalogues how android security has evolved over various versions of android. We strive to catalogue which version introduced a specific security feature or tweaked it as well as which version fixed a specific flaw.


|Android Version | Security Enhancement | Details | Reference / Bypass (if applicable) |
|---|---|---|---|
| 5.0  | Webview : de-coupled from core and OTA based upgrade  | WebView can now be updated independent of the framework and without a system OTA. This will allow for faster response to potential security issues in WebView  | [Chrome developers G+ Post][1] <br /> [WebView for android][2]  |
| 5.0 | Fixed : SQL injection vulnerability in WAPPushManager | In Android <5.0, a SQL injection vulnerability exists in the opt module WAPPushManager, attacker can remotely send malformed WAPPush message to launch any activity or service in the victim's phone (need permission check) | [Fixed commit][3] <br /> [POC : CVE-2014-8507 ][4] |
| 5.0 | Fixed : Privilege Escalation using ObjectInputStream | In Android <5.0, java.io.ObjectInputStream did not check whether the Object that is being deserialized is actually serializable. | [Fixed Commit][5]  <br/> [POC : CVE-2014-7911][6] |
| 5.0 | Fixed : SMS resend vulnerability | Applications can send SMS without privilege leading to undesired cost to user or be used for data exfiltration | [Fixed commit][7]  <br/>  [POC for CVE-2014-8610 ][8] |
| 5.0 | FORTIFY_SOURCE improvements | Protection against memory-corruption vulnerabilities involving stpcpy(), stpncpy(), read(), recvfrom(), FD_CLR(), FD_SET(), and FD_ISSET() libc functions |  |
| 5.0 | non-PIE linker support removed | Enhancing Address Space Layout Randomization (ASLR) by requiring all dynamically linked executables to support PIE (Position-Independent Executables) |  |
| 5.0 | Cryptography SSL/TLS | TLSv1.1 & TLSv1.2 are enabled, Forward Secrecy preferred and disabled weakcipher suits (MD5, 3DES) | [SSL Socket Reference : Android Developer Site][9] |
| 5.0 | Guest mode & multiple profile support | Guest mode and support for multiple user profiles Easier for providing easy temporary access to the device |  |
| 5.0   | Security Enhanced Linux (SELinux)                                  | SELinux Enforcing Mode is required for all applications on the device.  | |
| 5.0   | Full Disk Encryption by Default                                    | Devices shipped with Lollipop will have full disk encryption at first boot, using a unique key.                         | This feature can be turned off by Vendor's. |
| 5.0   | Smart Lock (screen lock)                                           | Unlock your phone using Bluetooth pairing, NFC, Geofence (GPS Location) or simply your smile (Face unlock improvements) |                                             |
| 4.4.4 | Block access to java.lang.Object.getClass in injected Java objects | Throws a java.lang.SecurityException on Browser UI thread when an attempt is  made to execute java.lang.Object.getClass from JavaScript code via an injected  Java object. | Refer : [Chromium BugTrack entry][10]  <br/>  [Chromium Issue entry][11] |
| 4.4.4 | Fix for OpenSSL man-in-the-middle | CVE ID : CVE-2014-0224 | Refer : [CVE 2014-0224 Entry][12] |
| 4.4.3 | Chrome Vulnerability Fix | 1\. timing-based security attack in Chrome2\. fix for CVE-2014-1710| [Chromium Bug Tracker Entry][13] <br/> Refer : [CVE 2014-1710][14] |
| 4.4.3 | Lock screen Credentials set vulnerability fix | As per Changelog :   Bug: 9858403 : lock screen credential reset w/o previous credentialsThe test asks the user to first set a lock screen password and then  launch an intent to change it, using an EXTRA that was not being properly  validated before the vulnerability was fixed. | reference : [AOSP Code Commit entry][15] |
| 4.4.2 | Removal of the "App Ops" application permissions control system | App Ops permission system which was available since 4.3 was removed completely from GUI in this release | Bypass : [Functionality launcher etc can be restored by an Xposed framework module][16] |
| 4.4 | dm-verity | transparent integrity checking of block devices. dm-verity helps prevent persistent rootkits that can hold onto root privileges and compromise devices. |  |
| 4.4 | SE_Linux => Enforced Mode | all root domain binaries are working in enforced mode. remaining still work in permissive mode | [SE Linux Details][17] | 
| 4.4 | FORTIFY_SOURCE | Level 2 : full source code compiled with FORTIFY_SOURCE and clang support added. | | 
| 4.4 | SSL CA Certificate Warnings | Warns when any certificate is added to the device certificate store | [Bypass available already][18] | 
| 4.4 | WRITE_EXTERNAL_STORAGE permission to write to SDCARD | This permission is required by applications in order to write to External Storage i.e. SDCARD. | [Android External Storage write permission ][19]  <br/> Also read [Storing app data on SD cards][20] | 
| 4.3 | Restrict Setuid from Android Apps | No Zygote spanned process is allowed to execute setuid program. /system is mounted with nosetuid | [Bypassed by Chainfire][21] | 
| 4.3 | FORTIFY_SOURCE | Android x86 and MIPS and fortified strchr(), strrchr(), strlen(), and umask() calls | | 
| 4.3 | SE_Linux => Permissive | allows logging but doesn't restrict actions  |  | 
| 4.3 | Trusted Platform Module (TPM) support | Hardware backed storage for KeyChain making keys unavailable for extraction | | 
| 4.2.2 | ADB Authentication | Prevents unauthorised use of ADB by the use of RSA keypair for authentication         | [Android 4.3 Security Enhancement Announcement][22] | 
| 4.2 | FORTIFY_SOURCE | Level 1 : This is used by system libraries and applications to prevent memory corruption | | 
| 4.2 | Application verification | user can opt for client side bouncer instance and google can verify malacious applications before installation. | | 
| 4.2 | Certificate Pinning | if chain of certs doesn't match an error message is added. | | 
| 4.2 | installd config | installd runs as non root from start. | | 
| 4.2 | ContentProvider security | by default contentprovider will be set to false for API <=17||
| 4.2   | init config | O_NOFOLLOW added to init to avoid symbolic link attacks.|
| 4.2   | premium SMS notification                            | SMS to premium numbers now display a notification and only allow needing when explicitely accepted.             |                                                                        |
| 4.2   | SecureRandom implementation                         | SecureRandom implementation based on OpenSSL, Bounty castle implementation removed.                             | [details here][23]                                                     |
| 4.2   | JavascriptInterface annotation | JavascriptInterface needs to be annotated for webview | exploit possible for <4.2 devices. and applications using API < 17  Reference : [Metasploit Module][24]  <br/>  [Test Page : identifies if browser or webview is vulnerable.][25]  <br/>  [Additional Details][26] |
| 4.2 | Cryptography | SSLSocket support for TLSv1.1 and TLSv1.2 using OpenSSL 1.0.1 |  |
| 4.1 | PIE (Position Independent Executable) support | Support for binaries compiled with GCC's -pie -fPIE flags  (executables to be position independent) |  |
| 4.1 | Read-only relocations / immediate binding | (-Wl,-z,relro -Wl,-z,now) |  |
| 4.1 | kernel address leakage prevention | dmesg_restrict and kptr_restrict enabled | kptr_restrict mitigates [Levitator Exploit][27] |
| 4.1 | ELF Hardening | RELRO / BIND_NOW flag default. This hardens those binaries against attacks that may attempt to overwrite the GOT and other sensitive ELF structures by making them read-only at startup. | [breaks Gingerbreak Exploit ][28]  <br/>  [more details on RELRO here ][29] |
| 4.1 | ASLR support | Full ASLR support |  |
| 4.0.3 | Randomize Heap/brk mapping | kernel.randomize_va_space is set to 2 |  |
| 4.0 | ASLR support | ASLR support started appearing although not fully. Multiple flaws were present dynamic linker didn't had ASLR and many more outlined in reference link | [ASLR support review by duo security][30] |
| 3.0 | full filesystem encryption | Full disk encryption added | [Details on this archive link][31] |
| 2.3 | format string vulnerability protection | added -Wformat-security -Werror=format-security |  |
| 2.3 | code execution prevention on stack and heap | Hardware-based No eXecute (NX) |  |
| 2.3 | null pointer dereference protection | mmap_min_addr |  |
| 2.2 | Device Administration | Android Device Administration API added | [Device Adminstration Guide][32] |
| 1.5 | Stack / buffer overrun protection | ProPolice to prevent stack buffer overruns (-fstack-protector) | [Memory Management Enhancement : Old Archive link][33] |
| 1.5 | Integer overflow protection | safe_iop |  |
| 1.5 | Integer overflow memory allocation | OpenBSD calloc |  |
| 1.5 | chunk consolidation attack | Extensions to OpenBSD dlmalloc() to prevent double free() |  |



This page is an ongoing effort and we will try to maintain it in up to date condition to the best of our abilities.

<strong>Credits :</strong>

This list is aggregated by <a href="http://anantshri.info" target="_blank">Anant Shrivastava</a> and <a href="http://prashantmahajan.wordpress.com/" target="_blank">Prashant Mahajan</a>. References where ever applicable are properly placed in the reference section.

Thanks to following folks for helping us with additional inputs.
<ul>
    <li><a href="http://ankurbhargava.com" rel="nofollow" target="_blank">Ankur Bhargava</a></li>
    <li><a href="http://manifestsecurity.com" rel="nofollow" target="_blank">Aditya Agrawal</a></li>
</ul>
Feel free to suggest corrections / additions in the list via either comments or a email to <a href="mailto:androidsecurityenhancement at tamerplatform dot com">AndroidSecurityEnhancement at androidTamer dot com</a>


[1]: https://plus.google.com/u/0/+GoogleChromeDevelopers/posts/Pb6BRDvRYVt
[2]: https://developer.chrome.com/multidevice/webview/overview
[3]: https://android.googlesource.com/platform/frameworks/base/+/48ed835468c6235905459e6ef7df032baf3e4df6
[4]: http://www.exploit-db.com/exploits/35382/
[5]: https://android.googlesource.com/platform/libcore/+/738c833d38d41f8f76eb7e77ab39add82b1ae1e2
[6]: http://www.securityfocus.com/data/vulnerabilities/exploits/71176.java
[7]: https://android.googlesource.com/platform/packages/apps/Mms/+/008d6202fca4002a7dfe333f22377faa73585c67
[8]: http://xteam.baidu.com/?p=164
[9]: https://developer.android.com/reference/javax/net/ssl/SSLSocket.html
[10]: https://codereview.chromium.org/213693005
[11]: https://code.google.com/p/chromium/issues/detail?id=359528
[12]: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0224
[13]: https://code.google.com/p/chromium/issues/detail?id=251711
[14]: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-1710
[15]: https://android.googlesource.com/platform/cts/+/0e2d6d9
[16]: http://repo.xposed.info/module/at.jclehner.appopsxposed
[17]: http://source.android.com/devices/tech/security/se-linux.html
[18]: http://forum.xda-developers.com/showthread.php?t=2533550
[19]: https://developer.android.com/reference/android/Manifest.permission.html#WRITE_EXTERNAL_STORAGE
[20]: https://support.google.com/android/answer/6046191
[21]: https://plus.google.com/+Chainfire/posts/WqS2E9kkN1L
[22]: http://source.android.com/devices/tech/security/enhancements43.html
[23]: http://source.android.com/devices/tech/security/dm-verity.html
[24]: https://github.com/jduck/addjsif
[25]: http://www.droidsec.org/tests/addjsif/
[26]: http://www.droidsec.org/news/2014/02/26/on-the-webview-addjsif-saga.html
[27]: http://jon.oberheide.org/files/levitator.c
[28]: http://c-skills.blogspot.com/2011/04/yummy-yummy-gingerbreak.html
[29]: http://isisblogs.poly.edu/2011/06/01/relro-relocation-read-only/
[30]: https://www.duosecurity.com/blog/a-look-at-aslr-in-android-ice-cream-sandwich-4-0
[31]: https://web.archive.org/web/20130129001617/http://source.android.com/tech/encryption/android_crypto_implementation.html
[32]: https://developer.android.com/guide/topics/admin/device-admin.html
[33]: https://web.archive.org/web/20130123122312/http://source.android.com/tech/security/index.html#memory-management-security-enhancements
