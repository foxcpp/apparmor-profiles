fox.cpp's AppArmor profiles
==============================

Vulnerabilities are everywhere and we have to deal with this mess. AppArmor
allows to enforce the principle of least privilege for each program you have to
run. This way it is possible to significantly reduce the possible impact of
security breaches.


Disclaimer
--------------

I wrote all profiles for my system (currently Arch Linux, Debian sid in past).
They may not work for your system. But... People publish things on GitHub to
make them accessible and usable by anyone, right? If something got broken on
your system and this problem is caused by my profile - please, open issue and I
will try to fix it.

Broken functionality
------------------------

I'm one of these people who often prefer security over usability. While it's
easy to cover all use cases for small applications like PDF viewer or IRC
client, it's nearly impossible to enumerate everything you may do with
bloatware like Firefox.  Also, if I will try to make sure every piece of code in
Firefox gets access to required resources it will open pretty big attack
surface. I don't want this.

**Note 1:** I made some restictions optional, always take a look at matching file
in `local/` if you think something important (like sound) is broken.

**Note 2:** This repository contains modified default "abstractions"
(`abstractions/gnome` and `abstractions/kde`), this may break other profiles.

How to use
--------------

1. Make sure `CONFIG_SECURITY_APPARMOR` is enabled in kernel configuration.
   This is default on Debian, Ubuntu and Arch Linux.

   You can use this command to check:
   ```
   zcat /proc/config.gz | grep "CONFIG_SECURITY_APPARMOR"
   ```

2. Add `apparmor=1 security=apparmor` to kernel command line.
   Depends on bootloader you use, check `/etc/default/grub` if you are using GRUB.

3. Install userspace AppArmor utilities.
   Package `apparmor` in Debian, Ubuntu, Arch linux.

4. Run `aa-status`. It should say "apparmor module is loaded".
   If it doesn't - make sure you updated bootloader configuration 
   (`grub-update`, `grub-mkconfig` probably) and reboot.

5. Copy contents of `profiles/` to `/etc/apparmor.d`.

6. Tweak files contained in local/ subdirectory (you probably don't want to
   skip it, default is very restrictive).

6. Load all AppArmor profiles
```
systemctl enable apparmor
systemctl start apparmor
```

Customization
--------------

Each system is different. Each user is different. You may want to allow more
than my profile allows. To do so, you need to add AppArmor rules to matching
file in `local/`. For example, to allow Firefox to access Downloads directory,
you need to edit `local/usr.lib.firefox.firefox` and uncomment mentioned
include statement.


Server profiles
--------------

I also have a set of profiles I use on my servers to sandbox stuff. It is in
server_profiles/.

License
--------------

Profiles I created from scratch are published under the MIT license.
Modified profiles from Ubuntu are published under the GNU Public License Version 2.
Check comments at beggining of each file if you care.

