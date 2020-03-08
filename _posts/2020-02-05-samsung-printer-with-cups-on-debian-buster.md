---
layout: post
title: Samsung printer with CUPS on Debian Buster
date: 2020-02-05 14:36 +0300
---

A few weeks ago, I was curious to run Samsung printer with CUPS on Debian 10.
Asked on the mailing list[^1]; however, there was no clear answer to this. That
was the goal, and the result is so far good. In the network, we have Microsoft
Windows 7 clients, and the mission was not just running the printer with CUPS:
clients need to connect to the CUPS machine--which makes sense, right?.

There will be two interesting parts in this blog: connecting the printer using
CUPS web interface and connecting a Windows 7 machine using CUPS.

I would like to mention that I am using Samsung SCX-6122FN model printer and
has static IP address on the local network. CUPS will reside on freshly
installed Debian Buster server. There is no other moving part in this setup.

This guide will not show you how to install CUPS because there are many of
them available online, like this guide. So, I highly recommend you to start
reading from the Debian Wiki page about CUPS[^2]. The Wiki page covers every
details you need to know about how to install and *configure* CUPS.

Also, I have got screenshots of every steps, so you can easily apply
instructions.

## Samsung printer on CUPS via web interface

You will need to use CLI just for now to allow local network admins to change
configurations through the web interface.

```bash
cupsctl --remote-admin --remote-any --share-printers
```

Now, we can get start to "Add a Printer". CUPS is already found some network
printers without needing to say the IP address of printer.

![List of discovered printers in CUPS web interface](/public/images/2020/002-discovered-printers-on-cups.png)

However, as you can see, I was not sure which printer is mine. So, I picked
the first one. I left the check mark of share this printer, and did changed
in the description field. Keep the printer name in your mind because you will
need in the last step, which is adding printer to the client.

![Add printer in CUPS web interface](/public/images/2020/003-add-printer-on-cups.png)

I could not find the model on this list, I jumped on the site called
OpenPrinter. The website provides scripts that are called PPD. I GRAB-ED the
PPD file that I need for this particular printer.

![Find model of printer in CUPS web interface](/public/images/2020/004-find-model-of-printer-on-cups.png)

I leave the default options for this printer as it is. CUPS part is just done.

## Adding shared printer on Windows 7

I would stop writing about this guide, but I had some "Bad & Hard Times" while
adding the printer which is managed under CUPS. The secret is in HTTP protocol,
the printer name you've assigned, and patience.

While the Windows wizard was looking for the printer, click the the "printer is
not in this list" button, so the wizard will allow you to use advance options
like using HTTP protocol to connect to the print server. Later on, you will
use a "web" address. The schema that CUPS use is

```
http://<IP_Address>/printers/<Printer_Name>
```

Now, you should see the result. Give it a try with sending a test page.

## Conclusion

> More screenshots are in the git repository

I have not seen a way that was seemingly configure printer on Linux before. I
always think that configuring a Linux server as a print server is a pain, but
it is not. I just spend an hour to do the print server and this guide. I also
curious how to get PDFs of faxes and photocopies. If one day I need to use
these functionalities, I definitely update this guide.

---

[^1]: ["Samsung SCX-6122FN on Buster" on debian-user list](https://lists.debian.org/debian-user/2020/01/msg00243.html)
[^2]: [CUPS](https://wiki.debian.org/SystemPrinting) on Debian Wiki
