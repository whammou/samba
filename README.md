# Samba-NAS setup

> Visit [Arch Wiki](https://wiki.archlinux.org/title/Samba) for more details

## Server

1. Configure Samba share from [Samba git config](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD)

2. Add samba group using 
`sudo group add -r sambausers`

3. add `User` mod 
`sudo usermod -aG sambausers <username>`
    * `-a` for add
    * `-R` supplementary group

4. Create password for the `group`
`sudo smbpasswd - a <username>`

5. Change ownership of `dir` to `group`
`sudo chmod -R :sambagroup /samba`

6. Change the permission of `dir`
`sudo chmod 1770 \samba`

7. Enable Samba Service `smbd.service`
`sudo systemctl enable --now smbd.service`
`sudo systemctl enable --now nmbd.service`

8. Done

## Client

1. Check id from the [`Server`](#server)
Running `id`
Output: `uid= gid= group=`

2. Mount Samba to desire `dir`:

`sudo mount //<adress>/sambashare /path/to/dir -o username=<username>,password=<password>,uid=<uid>,gid=<gid>,workgroup=<workdgroup>`
    1. Mount on boot, edit `/etc/fstab`
    `//ip/share   /home/whammou/server   cifs    _netdev,username=...  0 0`
    * To unmout
    `sudo umount server/`




