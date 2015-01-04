---
layout: post
title: "SSHLock Explained"
description: "SSHLock is a command-line utility I created after finding a bug in com.apple.purplebuddy."
category: articles
tags: [sshlock, iOS, iOS 8, explained]
image:
  feature: "techpaper3.jpg"
---

## SSHLock: The Name
SSHLock is called what it is because it can be used over `SSH` or SecureShell. SSH is a protocol that allows you to remotely execute code and transfer files over a wireless network. The package [OpenSSH](http://cydia.saurik.com/package/openssh/) enables this feature. Of course, you could always use an on-device application to execute this code such as [MobileTerminal](http://cydia.saurik.com/package/mobileterminal-applesdk/). But that would be silly because you have a lock button or AssistiveTouch right there. 

## How does it work?
SSHLock uses a feature inside com.apple.purplebuddy, or the Setup.app. If you hook into and read syslog's output as you lock the device, you will get something along the lines of: 

{% highlight c %}
Jan  3 20:25:51 Dayt0ns-iPhone backboardd[87] <Notice>: ALS: SetDisplayFactor: factor=0.0000
Jan  3 20:25:51 Dayt0ns-iPhone kernel[0] <Notice>: AppleMultitouchN1SPI: updating power statistics
Jan  3 20:25:51 Dayt0ns-iPhone SpringBoard[1305] <Warning>: [MPUSystemMediaControls] Disabling lock screen media controls updates for screen turning off.
Jan  3 20:25:51 Dayt0ns-iPhone backboardd[87] <Notice>: MultitouchHID: detection mode: 3->255
Jan  3 20:25:51 Dayt0ns-iPhone SpringBoard[1305] <Notice>: (Note ) MC: Locking device.
Jan  3 20:25:51 Dayt0ns-iPhone UserEventAgent[66] <Error>:  LockStateNotifier aksNotificationCallback posting notification: com.apple.mobile.keybagd.lock_status
Jan  3 20:25:51 Dayt0ns-iPhone UserEventAgent[66] <Error>:  LockStateNotifier aksNotificationCallback posting notification: com.apple.mobile.keybagd.lock_status
Jan  3 20:25:51 Dayt0ns-iPhone SpringBoard[1305] <Notice>: (Note ) MC: Locking device.
Jan  3 20:25:51 Dayt0ns-iPhone UserEventAgent[66] <Notice>: (Note ) PIH: Lock status changed.
Jan  3 20:25:51 Dayt0ns-iPhone UserEventAgent[66] <Notice>: (Note ) PIH: Lock status changed.
Jan  3 20:25:51 Dayt0ns-iPhone SpringBoard[1305] <Warning>: Telling backboard to enable secure lock screen.
Jan  3 20:25:51 Dayt0ns-iPhone SpringBoard[1305] <Warning>: Telling backboard to enable secure lock screen.
{% endhighlight %}

I was playing with Conrad Kramer's utility [Open](http://cydia.saurik.com/package/com.conradkramer.open/) and I found the bundle identifier for the Setup.app. Curious about what would happen if I opened an app that was only supposed to be opened once, I used Kramer's tool on the bundle identifier: com.apple.purplebuddy. While hooked into syslog and executing the program, I noticed that it printed out the same log as above. Seeing my oppritunity to create a program that would not inject foreign code and safely lock the device, how could I resist? I created the utility so it opens up com.apple.purplebuddy and then, 0.5 seconds later (after lock process has been initiated), it kills Setup.app. So when you unlock your device, there is no trace of it ever being opened and you feel safe.

#### Number of Times SSHLock Has Been Downloaded:
<p></p><script type="text/javascript" src="http://modmyi.com/cstats/index.php?package=com.dayt0n.sshlock&output=text"></script>

### -dayt0n