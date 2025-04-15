# pearity
10 inch Rack Mountable 8 bay Thunderbolt JBOD

<img width="1114" alt="Screenshot 2025-04-04 at 8 13 20 PM" src="https://github.com/user-attachments/assets/d3d1c9c0-4876-4bec-b926-8fc372e995e5" />
<img width="1128" alt="Screenshot 2025-04-04 at 8 40 01 PM" src="https://github.com/user-attachments/assets/3383ddb6-2c79-4624-aa3c-b2c272ee415c" />
<img width="1066" alt="Screenshot 2025-04-04 at 8 35 10 PM" src="https://github.com/user-attachments/assets/e3912d3e-6d6a-4a09-a806-5595236a8b51" />
<img width="1090" alt="Screenshot 2025-04-04 at 8 15 51 PM" src="https://github.com/user-attachments/assets/bd937b18-66fd-48db-80de-05e6691889e4" />



I’ve finished the initial design of my 3D-printable 10-inch rack-mountable 8-bay JBOD with backplane! That’s a mouthful. Someone suggested the name Pearity so now I'm running with it. This project is how I’ve been teaching myself fusion360, so it’s far from perfect, but I’m learning fast. I got the initial files for this project from Rio Li on MakerWorld: https://makerworld.com/en/models/1229874-10-inch-rack-8-3-drives-bay-jbod#profileId-1248465

I recently upgraded my main server to a Mac Mini. Great machine, super-fast and power efficient, tiny footprint. Only downside is no expandable storage. Thankfully it has 4 Thunderbolt ports offering 40Gbps. I don’t need the super high speeds as I’m only wanting to add spinning drives.

The downside I’ve found with Thunderbolt is its cost. I couldn’t find any enclosure that looked trustworthy online for less than $50, and those are enclosures for m.2 drives. If I want a Thunderbolt enclosure for spinning rust then my options start at about $300 for two bays and $750 for an 8-bay. Ouch. And it won’t fit in a 10” rack.

I set out to design something with features similar to the OWC Thunderbay Flex 8 but quickly ran out of room and went over budget. I want an additional ethernet port on my Mac Mini, but does it really need to be part of the JBOD? Do I need to have my solid-state storage in the same box as my spinning rust? Would I really use additional USB ports? And what use is a DP port on a rack-mounted box? So, I scrapped the original Orico dual m.2 enclosure and dock I’d chosen and went with a smaller, simpler, and cheaper option.

There are three big components to print: the main body, the back panel, and the front panel, plus the 8 drive caddies. The widest a piece will be is 255mm, I designed this to print on beds of 256x256x256mm or bigger.

Things to note:

Currently the back offers no structural support even though it has rack ears. I plan to integrate a support system in the future. I also haven’t finalized a way to attach the back, this will be part of the support system. I’m trying to figure out a way to make the length variable so it can fit in different depth racks. 

Also, my plan is to tie the electrical lines for the fans together on the back panel and have them connect to the body with pogo pins. The fans are attached to the back with printed TPU.

The front panel/faceplate slides in to the main body with extremely tight tolerances, hopefully it doesn’t need a clip to stay in place. Once I figure out the LED connector on the backplane, I plan to run a cable thru to the faceplate and modify the faceplate with micro holes above each drive with an LED behind them to indicate activity status. Right now, the faceplate is just an extra piece but I have plans to add features.

The main body needs to be printed in something strong and heat resistant, don’t expect PLA to hold up.

The backplane is 0.9mm too long. You need to carefully sand/grind off material on one edge until you are able to slide it in. There are no components to damage in this .9mm.

The spacing for the SATA connectors on the backplane is 27.5mm. The spacing of the hard drives is 27mm. This results in some strain on the connectors. Frequent swapping of drives might result in eventual physical damage of the drive connectors. I will likely redesign this to be a 7-bay holder using the same backplane with one of the slots on the board left open to provide a more friendly option for frequent swaps.

There is VERY little space for airflow. Thinner hard drives will allow more airflow which will in turn allow lower temperatures leading to longer life. 

I have the body, faceplate, and caddy files ready to print, but I need better measurements of the Acasis thunderbolt controller and the location of the TB port on it as well as where the mini-SAS headers are when the HBA card is plugged into the m.2 slot. Once I have these measurements I’ll finish the back panel. Right now the USB-C hole on the back is only approximate.


Materials:

I’ve revised my initial bill of materials to be a bit more budget friendly. My initial cost was approaching the cost of an OWC Thunderbay.

For Thunderbolt control I’m using the ACASIS 40Gbps M.2 NVMe SSD Enclosure, which is only compatible with TB3, TB4, and USB4. Don’t try to use this with USB 3.2. 40Gbps = 5GBps. 

Connecting to the m.2 slot on the TB controller I have an 8-port PCIe 3.0 x2 controller, which should be able to hit 1700MB/s. 1700MBps = 13.6Gbps = 1.7GB/s. Not fast enough for some speed freaks here, but more than enough to saturate my network. Network is usually the bottleneck from what I can tell. Another option I considered, if you only want 6 drives instead of 8, is this m.2 to 6 slot SATA board that promises 16Gbps = 2GBps. 

I’m connecting the SATA controller to an 8-bay backplane. I contacted half a dozen different sellers on AliExpress that have a similar looking black 8 bay SATA backplane asking for schematics. The ones that responded all sent the same schematics. I am 90% certain this is the SATA backplane used in the Jonsbo cases. Even if it’s not, it has the same dimensions. It’s cheap, easy to source, and has a record of being semi-reliable. Not expecting enterprise grade reliability from a sub-$20 board. Available on AliExpress for $15 including shipping. I used Lesozoh Technology Store, store number 1102843659, if you want to make absolutely certain you use the same board.

To power everything I was initially looking at PC power supplies. However, I felt like the sizes available weren’t great for the constraints of this project. I’ve decided to go with a 12V 300w LED power supply. Somebody tell me why this is a bad idea. Seriously. It’s more compact than any 300w PC power supply, it’s rated for way more than I’ll be using, and it’s cheap.

To get the 5V I will also need from the LED power supply, I’ll use a 30A 150W buck converter. This is only half the wattage my PSU puts out, am I gonna explode?

To keep cabling mess to a minimum, I’ll be using these lever wire connectors. The PSU has two lines for out: one line out will be routed to one of these connectors/splitters which will split off to the SATA power connector and IDE power connector on the backplane as well as the fans; the other line out will first go to the buck converter, then to a second lever connector, then from there to the backplane. I’m considering using more of these splitters to provide 5V/12V power on the back for any devices on my rack that might need it.
