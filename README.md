fox.cpp's AppArmor profiles
==============================

Vulnerabilities are everywhere and we have to deal with this mess. AppArmor
allows to enforce the principle of least privilege for each program you have to
run. This way it is possible to significantly reduce the possible impact of
security breaches.


Disclaimer
--------------

I wrote all profiles for my system (Debian testing). They may not work for your
system. But... People publish things on GitHub to make them accessible and
usable by anyone, right? If something got broken on your system and this
problem is caused by my profile - please, open issue and I will try to fix it.

Broken functionality
------------------------

I'm one of these people who often prefer security over usability. While it's
easy to cover all use cases for small applications like PDF viewer or IRC
client, it's nearly impossible to enumerate everything you may do with
bloatware like Firefox.  Also, if I willtry to make sure every piece of code in
Firefox gets access to required resources it will open pretty big attack
surface. I don't want this.

**Note 1:** I made some restictions optional, always take a look at matching file
in `local/` if you think something important (like sound) is broken.

How to use
--------------

To get AppArmor working you need two things: Kernel module and a set of
userspace utilities. For first probably you have to compile your own kernel,
but some distributions ship kernel with AppArmor enabled (Debian and Ubuntu are
one of these). Anyways, make sure `CONFIG_SECURITY_APPARMOR` is enabled in
kernel configuration. Then look for apparmor package in your distribution
repositories.

Run `aa-status` and make sure it says `apparmor module is loaded`.

Copy contents of `profiles/` to `/etc/apparmor.d`.

Enable and start AppArmor service to load all profiles during boot.
```
systemctl enable apparmor
systemctl start apparmr
```

Customization
--------------

Each system is different. Each user is different. You may want to allow more
than my profile allows. To do, so you need to add AppArmor rules to matching
file in `local/`. For example, to allow Firefox to access Downloads directory,
you need to edit `local/usr.lib.firefox.firefox` and uncomment mentioned
include statement.

License
--------------

Generally I do not care about usage of things I publish on GitHub but I have to
because of laws. MIT have created pretty good permissive license that allows
any usage as long as you keep copyright notice.

