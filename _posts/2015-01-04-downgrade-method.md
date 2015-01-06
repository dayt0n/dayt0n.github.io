---
layout: post
title: "Downgrade Method"
description: "Over Christmas break, I found a method to tether downgrade an iPhone 4."
category: articles
tags: [downgrade, iPhone 4, limera1n, redsn0w, iFaith, iTunes]
image:
  feature: techpaper4.png
---

## Disclaimer
I am not responsible for any damage that may occur if you do not follow these directions correctly. I am also currently fixing the only bug I have found so far. Please [tell me about any bugs you find](mailto:daytonhasty@gmail.com?subject=Downgrade%20Bug).

## 1. Preparation
First, please do a fresh restore on your phone with a default, signed iPSW. Set it up and then continue. To configure your iTunes to accept the downgrade ipsw, you must install iTunes 11 ([32 bit](http://api.ios.icj.me/v2/iTunes/Windows/11/url/dl) | [64 bit](http://api.ios.icj.me/v2/iTunes/Windows/11/64biturl/dl)). Once the iTunes 11 installer has downloaded, go into your Music folder and you will find the iTunes folder. Rename it to iTunes_orig. Then, you must go to ControlPanel>Uninstall a Program. Uninstall iTunes. Then run the iTunes 11 installer. 

Next, you will need to download the following items. Unzip if it is a zip file. I suggest you keep them on your desktop to have them easily accessible:

* <a href="https://ipsw.me" target="_blank">The iPSW file you want to downgrade to</a> (Select iPhone 4 Model) If you are downgrading to iOS 6, download the <strong>6.0</strong> iPSW, not the one you want to downgrade to. 
* [iReb](https://github.com/iH8sn0w/iREB-2.0/releases/r7/1097/ireb-r7.zip)
* [Redsn0w 0.9.15 Beta 3](http://www.jailbreaktools.com/downloads/windows/redsn0w-0.9.15b3.zip)
* [iFaith](https://github.com/iH8sn0w/iFaith/releases/v1.5.9/1085/ifaith-v1.5.9.zip)
* [Request Universal SHSH Blobs](mailto:daytonhasty@gmail.com?subject=SHSH%20Blob%20Request&body=Please%20write%20iPhone%204%20model%20number%20found%20in%20Settings>General>About>Model.%20Also%20include%20the%20iOS%20firmware%20you%20want%20to%20downgrade%20to.)

## 2. Downgrade iPSW Creation
Now, fire up iFaith and select `OK` and then `Build *signed* IPSW w/ Blobs`. Click `Browse for SHSH Blobs` and select the universal blob I sent you after you requested it from me. iFaith will verify the blob and take you to a screen asking you to either `Browse for an IPSW` or `Download it for me`. Click `Dowload it for me`. After it is done downloading, it will build the downgrade iPSW file. It will then bring you to a screen telling you that iFaith has successfully built your iPSW file. Click `Ok`. iFaith will then display a window with a picture of an iPhone turning off. You can exit out at this point and continue to the next step.

## 3. Enter PWNed DFU Mode
Plug your phone into your computer. If iTunes opens, exit out. Turn off your phone. Then, open up iReb and select iPhone 4 and follow the instructions to enter DFU Mode. DFU Mode looks like a blank screen on your phone. Next, iReb will exploit your phone using the [limera1n](http://dayt0n.github.io/articles/what-is-limera1n/) exploit and your phone will enter PWNed DFU Mode. PWNed DFU Mode looks the same as DFU Mode. Once this is done, open up iTunes and it should tell you the iPhone is in Recovery Mode. This is good.

## 4. Downgrade!
Now, hold down the Shift key and click `Restore iPhone`. Select the iFaith iPSW file you built earlier and the downgrade should start. <strong>Note that this does erase all content on the iPhone.</strong> You can exit out of iReb now. Now, just wait until the progess bar on the iPhone fills completely and iTunes either gives you an error at the end of the restore or a message saying the restore was completed. If you do get an error at that point, then it doesn't matter, the downgrade has worked. Your phone should now either boot back into DFU Mode or Recovery Mode. It should not go into userland. You can exit out of iTunes now. 

## 5. Boot!
As I said before, this is a tethered downgrade meaning you have to boot the iPhone up from the computer every time you turn it off and back on again. You should now open up the redns0w application. Now, if your phone is in Recovery Mode (the iTunes Logo with a cable under it), put it into DFU Mode. If you need help, use <a href="http://www.jbfaq.com/article.asp?id=60" target="_blank">this article</a>. Otherwise, your phone should be in DFU Mode already if it is not in Recovery Mode. Select `Extras`. Click `Select iPSw` and select the iPSW file you downloaded in the first section of this article. Redsn0w should tell you that it has successfully identified iPSW. Now, in redsn0w, select `Just Boot`. Remember, since this is tethered you must repeat this step everytime you reboot/turn it on after a power off or dead battery. 

<center><h1>Congrats, you just downgraded :)</h1></center>

# Technical Details
For people who would like to verbose boot instead of just a pineapple bootlogo, you can open Redsn0w, select `Extras`, `Even more`, `Preferences`, `Boot args`, and type in `-v`. Then, when you boot with redsn0w, you get a verbose boot.

#How it Works
Every time an iOS device restores/boots with iTunes, it checks the random `nonce` string generated at boot. If everything checks out, then the APTicket is sent from iTunes servers and the restore is given the okay to continue. If the `nonce` string does not check out, then the restore will fail, making downgrading impossible if you use a default iPSW because iTunes does not find the APTicket for that particular `nonce` initiation. With this method, the using a universal SHSH blob, the restore checks out and iTunes likes the iPSW from iFaith. But it is tethered because as soon as you power it back on, another random `nonce` string is generated and the device will refuse to boot. That is why you use redsn0w to exploit it with [limera1n](http://dayt0n.github.io/articles/what-is-limera1n/) and forcefully boots it. This method does not jailbreak it, but gives you the option to. If you would like to jailbreak it, just use redsn0w. <strong>This method works also on an iPod touch 3rd generation by the way.</strong> 

## Overview
I have been using this method on my iPhone 4 (3,3) to have iOS 6.1.2 on it. I personally like iOS 6 on an iPhone 4 just because it is so much faster and fluid than iOS 7. iOS 7 is too laggy and heavy on the iPhone 4. Don't worry, if this method seems too difficult, just know that I am working on a way to fix the bugs I have told you about and just have you boot into PWNed DFU Mode and restore with iTunes and boot with redsn0w. I will basically just start mass producing iPSW files for every firmware of every iPhone 4 and iPod touch 3rd generation. Sound off in the comments about what you think of this tutorial. And as for an untether, I have enough work as it is with making this simpler and with school. An untether is not off of my to-do list though, I will tell you that :)

# Credits
* <center>Thanks to [CPVideoMaker](https://twitter.com/CPVideoMaker) for help with SHSH blobs and bug aid</center>
* <center>Thanks to [iH8sn0w](https://twitter.com/iH8sn0w/) for iReb and iFaith</center>
* <center>The [iPhone Dev Team](https://twitter.com/iphone_dev) for redsn0w</center>

<center><h3>-dayt0n</h3></center>
