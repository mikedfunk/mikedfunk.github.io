---
layout: post
title: Automounting With Virtualbox
---

While I work on learning [Vagrant](http://vagrantup.com) and [Puppet](http://puppetlabs.com) I am using a manually built VM for development. I thought it would be cool to just mount a directory from my mac to the Ubuntu `/var/www`. This way I can set my `/etc/hosts` file on my mac to point a domain to my VM, set up a vhost on that VM, ssh into the VM, and work and preview remotely. Doesn't sound too difficult right?

Wrong.

<!--more-->

[Virtualbox](http://virtualbox.org) has an option to automount a share. Cool! Let's see, should be easy. Select a machine, click settings, click shared folders, click the plus icon, and here's what we get:

![Shared Folder Options]({{ site.url }}/public/images/vbox_shared.png)

**Wat.** Is that the path to the local folder or the guest? Who cares what it is called? I just want it to show up in a guest directory. So we save this and start up. Guess what? Nothing, because there was no option to specify the destination directory. Instead it gets mounted to `/media/sf_{mount_name}` on the guest disk. How the hell do I get it to show up in a directory of my choosing on the guest instead?

## Ubuntu 13.10 Instructions

In Ubuntu, we've only made it half way. Here's how to finish the job.

1. Fill in the shared folder options with the path to the share *on the host machine* and give it a name. Save and restart.
1. Symlink `/media/sf_{mount_name}` to `/var/www` assuming you want the destination mount to be /var/www
2. Append the line `vboxsf` to `/etc/modules` so it is able to mount when you start up
3. Append this line to `/etc/fstab`: `{mount_name}       /var/www   vboxsf  defaults     0   0` **Be sure to copy the spaces exactly!** The spaces are used to delimit options in fstab. I know, O_O.
4. Add your user to the vboxsf group: `sudo usermod -a -G vboxsf {username}` so you can access the directory
5. Add the apache user to the vboxsf group: `sudo usermod -a vboxsf www-data` so apache can serve the files
5. Restart

Done! Now it should mount when we start up! Now why can't I skip all this crap and just do it in the VirtualBox gui?
