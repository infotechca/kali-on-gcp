# How to Upload or Install Kali Linux on Google Cloud
## _Steups to do_
**Ctrl+Click** [Google Cloud Help!](https://cloud.google.com/compute/docs/import/import-existing-image)
- [x] 1. Prepared your system in a VirtualBox environment
- [x] 2. Configure SSH or user login access on the image
- [x] 3. Convert a .vdi or .qcow2 disk image to disk.raw format
- [x] 4. Compress the disk image file
- [x] 5. Create a bucket and upload the file
- [x] 6. Import the image to your custom images list
- [x] 7. Test the imported image to ensure it works
- [x] 8. Setup GUI Remote access to Linux using NoMachine
---
### 1. Prepared your system in a VirtualBox environment
#### 1.1 - Create Virtual Machine
1. Name: Kali
2. Type: Linux
3. Version: Debian (64-bit)
#### 1.2 - Create Virtual Hard Disk
* File Size: 20GB
* HDD file type: QCOW (QEMU Copy-On-Write)
#### 1.3 - Settings
- System > Motherboard > Boot Order: Uncheck Floppy
- Network > Adapter 1 > Advanced > Adapter Type: Paravirtualized Network (virtio-net)
#### 1.4 - Partition Disk: Manual
![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) **_Important Steps_: otherwise, it will not work.**
1. Select your Hard disk and click Continue
2. Create new empty partition table on this device? – `Yes`
3. Select: `> pri/log 20 GB FREE SPACE` and Click Continue
4. Select: `Create a new partition` and Click Continue
5. New Partition Size: `max` and Click Continue
6. Type for the new partition: `Primary` and Click Continue
7. Select: `Done setting up the partition` and Click Continue
8. Select: `Finish Partitioning & write changes to disk` and Click Continue
9. Do you want to return to the partitioning menu? – `No`
10. Write the Changes to disks? – `Yes`
---
### 2. Configure SSH or user login access on the image
Login with created user during installation.<br/>
In my case: User: `haseeb` Pass: `infotech`<br/>
- _Open up the Terminal._

#### 2.1 - Set root account password.
```bash
sudo -i
passwd
New Password: toor
Retype New Password: toor
```
#### 2.2 - Change the SSH configuration file and Un-hash (#) these two entries
```bash
nano /etc/ssh/sshd_config

PermitRootLogin yes
PasswordAuthentication yes
```
**Ctrl+o** to save changes and hit `enter`<br/>
**Ctrl+x** to exit
#### 2.3 - Permanently enable the SSH service to start on every reboot.
```bash
systemctl enable ssh.service
systemctl start  ssh.service
systemctl status ssh.service
```
##### Make sure you have SSH access: `root` account
```bash
ssh root@localhost

Are you sure you want to continue connecting (yes/no/[fingerprint])? Yes
root@localhost’s password: toor
root@kali:~# exit
```
##### Make sure you have SSH access: `user` account
```bash
ssh haseeb@localhost

Are you sure you want to continue connecting (yes/no/[fingerprint])? Yes
haseeb@localhost’s password: infotech
haseeb@kali:~# exit
root@kali:~# poweroff
```
---

### 3. Convert a .vdi or .qcow2 disk image to disk.raw format
Open Windows Command Prompt: `Win+R` then type `cmd`<br/>
```cmd
cd "\Program Files\Oracle\VirtualBox"
c:\Program Files\Oracle\VirtualBox>
```
#### Convert .qcow disk image to disk.raw format
**Syntax**: `VBoxManage clonemedium guest-image ~/disk.raw --format RAW`<br/>

In my case source locations: `h:\0-VirtualBox\Kali\Kali.qcow` Destination location `f:\disk.raw`<br/>

![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) **_Very Important_**: do not rename `disk.raw` to any other name but `disk.raw`
```cmd
c:\Program Files\Oracle\VirtualBox>
VBoxManage clonemedium  h:\0-VirtualBox\Kali\Kali.qcow f:\disk.raw --format RAW
```
![Convert .qcow disk image to disk.raw format](https://github.com/infotechca/kali-on-gcp/blob/master/convert.png)

---
### 4. Compress the disk.raw image file
On Windows Open up your WSL Linux or WSL Ubuntu.<br/>
If you do not have **WSL Linux**, installed first, we are going to use `tar` for compression.<br/>
Change directory to `disk.raw` file location: In my case
```bash
cd /mnt/f/
tar --format=oldgnu -Sczf kali-image.tar.gz disk.raw
```
![Compress the disk.raw image file](https://github.com/infotechca/kali-on-gcp/blob/master/compress.png)

![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) **Important**: do not rename `disk.raw` otherwise it will not work.

### Complete Video Tutorial on [YouTube.com/infotechca](https://www.youtube.com/watch?v=QiBPJICfcMw)
[![Click here to watch on YouTube.](http://img.youtube.com/vi/QiBPJICfcMw/0.jpg)](http://www.youtube.com/watch?v=QiBPJICfcMw "How to Upload or Install Kali Linux on Google Cloud 100% Work!")
---
▀▄▀▄▀▄ [ Follow us on ] ▄▀▄▀▄▀<br/>
Website:    https://www.infotechca.com<br/>
YouTube:    https://youtube.com/infotechca<br/>
Twitter:    https://twitter.com/infotechca<br/>
Facebook:   https://www.facebook.com/infotechca.hyd<br/>
Instagram:  https://www.instagram.com/infotechca<br/>
Pinterest:  https://pinterest.com/infotechca<br/>
Github:     https://github.com/infotechca<br/>
