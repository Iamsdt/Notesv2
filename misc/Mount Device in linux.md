---
Created by: Shudipto Trafder
Created time: 2023-12-11T23:32
Last edited by: Shudipto Trafder
Last edited time: 2023-12-12T16:17
tags:
  - linux
  - storage
---

Great to hear that step 2 worked for you! Here’s a quick recap of what likely resolved the issue:

1. **Install ntfs-3g**:
   ```sh
   sudo pacman -Syu ntfs-3g
   ```

2. **Manually Mount the NTFS Partition**:
   ```sh
   sudo mount -t ntfs-3g /dev/sda2 /mnt
   ```

If you need to mount this partition automatically in the future, you can add an entry to your `/etc/fstab` file. Here’s how to do it:

1. **Edit /etc/fstab**:
   Open `/etc/fstab` in your preferred text editor:
   ```sh
   sudo nano /etc/fstab
   ```

2. **Add the NTFS Partition**:
   Add a line for the NTFS partition. Replace `/mnt` with your preferred mount point if necessary:
   ```sh
   /dev/sda2   /mnt   ntfs-3g   defaults   0   0
   ```

3. **Save and Exit**:
   Save the file and exit the text editor. For nano, you can do this by pressing `Ctrl+O` to save and `Ctrl+X` to exit.

4. **Mount All Filesystems**:
   To test the changes without rebooting, run:
   ```sh
   sudo mount -a
   ```

This should automatically mount the NTFS partition at boot.

If you have any further questions or run into any more issues, feel free to ask!