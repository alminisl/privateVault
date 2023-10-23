- [POSTS](https://eliaslundgaard.com/posts/)

### How to Mount Synology NAS to Raspberry Pi

#### May 2, 2021    guides

You’re probably here because you’ve spent more than five minutes trying to figure out how to mount your new Synology NAS to your Raspberry Pi. Even though it’s basically the same as mounting any other drive, there’s a couple of details you need to take care of. I’ll walk through the entire process here.

## The Use Case

I recently acquired an old Synology NAS running Synology DiskStation to keep extra back-ups of cloud storage (better safe than sorry), TimeMachine and to host some of my music & media which can then be accessed through services like Plex.

## Create the folder

To begin with, create a [Shared Folder](https://www.synology.com/en-us/knowledgebase/DSM/help/DSM/AdminCenter/file_share_create) in Synology DiskStation. I called mine `music`.

In this guide, we will access the Network Drive through the [Network File System (NFS)](https://www.geeksforgeeks.org/difference-between-nfs-and-cifs/) protocol. It’s easy to set up, but not very secure. So if your data is sensitive, or you don’t feel like sharing your playlist, you should probably use something like CIFS instead.

Go to your DiskStation dashboard, and head to **Control Panel -> Shared Folder -> {Your Drive} -> Edit -> NFS Permissions** and click **Create**.

I use the following settings:

<img width="740" height="644" src="../../../../_resources/edit-nfs-rule_c070df1b939844079054b37d29dde737.png"/>

- **Hostname or IP** Here, I’m using the wildcard (*) to allow access from all devices on the network, since my music is not sensitive data. You can also supply your Pi’s or Plex server’s IP to tighten security just a bit.
- **Privilege** is read-only since I don’t want anyone to delete or edit my music.
- **Squash** means that all incoming users can be mapped to a certain set of permissions attached to an existing user on your NAS. This is important, since it allows us to connect without user credentials.

When done, click **OK** twice to apply changes.

## Connect your Pi

`SSH` into or open your Pi’s terminal. Create your mount point with whatever name you want, fx NAS:

```
sudo mkdir /mnt/NAS 
```

Now you need your Synology NAS IP (can be found in DiskStation) and your folder’s Mount Path which can be found in the **NFS Permissions** from before, in the bottom (see screenshot above). Mine is /volume1/music.

We can now mount the folder:

```
sudo mount -t nfs {SYNOLOGY_IP}:{MOUNT_POINT} /mnt/NAS 
```

[[linking PI and Synology]]

for example `sudo mount -t nfs 128.0.0.165:/volume1/music /mnt/NAS`. And voilà! You should now be connected.

* * *

##### Related Posts

* * *

© All rights reserved. Powered by [Hugo](https://gohugo.io/) and [sustain](http://www.github.com/nurlansu/hugo-sustain/) with ♥