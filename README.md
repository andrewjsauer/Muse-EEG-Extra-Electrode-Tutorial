# 2016 Muse EEG Headset: Making an Extra Electrode

This is a guide for making your own auxiliary electrode for the Muse 2016 EEG headset. 

These auxiliary electrodes can be used to measure a variety of signals from any area of the head and body. For example, ECG from the chest, EMG from the neck or arms, EOG from around the eyes, or EEG from different sites on the scalp that the standard Muse electrodes do not reach (think Oz / Cz, or back of the head / top of the head). 

With that said, the purposes of this guide is making an extra EEG electrode for the 2016 Muse headset. Additionally, with the intention of making 3-4 of these electrodes, the total cost (itemized in the components section) was roughly $42 after tax / shipping. Lastly, the only requirement is to know how to solder. Enjoy!

# Introduction
Hey! Thanks for checking out this tutorial, I hope you find it useful and if you have any recommendations, questions or comments, please reach out! 

I am one of the organizers of a kickass group [NeuroTechLA](https://www.meetup.com/NeuroTechLA/), the Los Angeles chapter of [NeuroTechX](https://neurotechx.com/community/), a global network of engineers, designers, scientists, and hackers driven to learn and push forward the boundaries of bona fide neuroTechnology. If you're new to this field and interested in getting started with brain-computer interfaces (BCI) or electroencephalography (EEG), checkout NeuroTechEDU's GitHub repo of [awesome list of BCI-related resources](https://github.com/NeuroTechX/awesome-bci). Or, attend one of the events that we might be holding in your city!

This tutorial is the result of our chapters desire to do BCI-related projects with Muse headsets. Specifically, we wanted our chapter to go through workshops like this [P300 ERP Juypter Notebook](https://eeg-notebooks.readthedocs.io/en/latest/) experiment using an extra electrode and many more. There were a few [tutorials](http://forum.choosemuse.com/t/step-by-step-tutorial-for-making-muse-auxilliary-channel-electrode/3172) and [forum discussions](http://forum.choosemuse.com/t/obtaining-an-auxiliary-sensor/1348) on how to make these extra electrodes, but I found them a little bit incomplete and inaccessible. 

Lastly, special thanks to [Interaxon](https://choosemuse.com/), the company responsible for the Muse headsets, for donating a couple headsets to our chapter! They, along with the many members of NeuroTechX, made this possible. 

**Disclaimer**
* This is not an official Interaxon tutorial;
* DO NOT plug the electrode into a power source;
* Use caution and be safe! 

# Goal
Our goal in this tutorial is to connect an EEG electrode via a male Micro USB connector to the auxiliary input of our 2016 Muse headset (the back right of the headset where you would charge the device) so we can access EEG (or EMG / ECG, etc.) data. 

We will do this by removing the safety jacket and exposing wire from our lead EEG cable, solder said wire onto a 5-pin Micro USB connector, wrap with heat shrink, snap the Micro USB plastic covers on, attach hook & loop fasteners to our headset for keeping the electrode stable while recording, snap on a electrode to our cable lead and test using Python and the [muse-lsl library](https://github.com/urish/muse-lsl-python).

## Instructions
Note: We assume you know how to solder, or you know someone who can help you. If not, soldering kits are ~$30 on Amazon. 

### Step 1 
Purchase and gather necessary supplies and equipment. Below is a photo of everything I used (Muse headset, 3rd arm clamps for soldering and wire cutters not shown).

![Image of tools used](https://cdn.hackaday.io/images/5482501541302151684.jpg)

1. Heat shrink for wrapping the Micro USB connector in
2. Lead wire for EEG electrodes
  * Since we are only removing the safety jacket (the end of our wire) we can use any electrode wire such as an OpenBCI snap electrode   cable, gold cup cable, etc.
  * In this tutorial, we will be using a lead wire designed for snapping on dry EEG electrodes as shown above.
3. EEG dry electrode (pack of 10+)
  * As noted above, we could have used gold cup electrodes (which can be referred to as wet electrodes which means they would require conductive paste), or EMG / ECG foam solid gel electrodes that would have been used with snap electrode cables.
  * In this tutorial, we will be using dry EEG electrodes that will snap onto our lead wire.
4. 60/40 Flux Core Solder
5. Soldering Iron (best practice is use a temperature controlled soldering iron, the one shown above is not)
6. Wire Strippers
7. Hook and loop (think Velcro) straps
  * Shown in the photo as a roll next to the adhesive hook and loop stickers.
8. 10 Piece 5-Pin Micro USB Type B Male Connectors with Plastic Cover Kit 

See this [components section](https://hackaday.io/project/162169/components) in this project for details on where these items where purchased and the costs.

### Step 2: Wire Preparation
Take your EEG lead wire and remove the safety jacket (circled in green) by giving it a tug, which should expose about 1 to 7 mm of wire. Or cut close to the safety jacket and use your wire strippers to expose the wire.
  * Note: At any point in the following next steps should an error arise (like using too much solder, etc.) simply snip off the wire, use your wire strippers to expose a little bit of wire and come back to this step. 

![Remove EEG safety jacket](https://cdn.hackaday.io/images/5656511541304127814.jpg)

Secure the wire for the next step and if applicable snap your EEG electrode on.

![Secure wire for next step](https://cdn.hackaday.io/images/9683641541190757314.jpg)

### Step 3: Soldering to Micro USB
Now, the next step will be to solder the exposed end of the wire to a male Micro USB connector. According to Sam from Interaxon, this connection needs to be made specifically on pin 4 on the  Micro USB 5-pin layout.

But where's pin 4?

![USB pins](https://cdn.hackaday.io/images/4363041541305003115.jpg)

Cool, that's pin 4, but what do these pins mean? According to Wikipedia:

Pin | Name | Wire color | Description
----| -----| ---------- | -----------
1 | VBUS | Red | + 5 V
2 |	D-	 | White |	Data- 
3	| D+	 | Green |	Data+
4	| ID	 | N/A	 |  Permits detection of which end of a cable is plugged in, "A" connector (host): connected to the signal ground, "B" connector (device): not connected
5	| GND	 | Black | Signal ground

Cool, I think we can intuitively understand data, ground and power, but ID? (Though D- and D+ are kinda confusing so [here's](https://electronics.stackexchange.com/questions/20023/why-does-usb-have-4-lines-instead-of-3#answer-20025) a nice description of Data+ and Data-)

According to this [StackExchange answer](https://electronics.stackexchange.com/questions/35462/why-does-micro-usb-2-0-have-5-pins-when-the-a-type-only-has-4), this extra pin which is used as of late 2001 is also called On-The-Go (OTG) which is used to select which device is the host or slave, or as [Wikipedia](https://en.wikipedia.org/wiki/USB_On-The-Go) puts it,

>USB On-The-Go, often abbreviated to USB OTG or just OTG, is a specification first used in late 2001 that allows USB devices, such as >tablets or smartphones, to act as a host, allowing other USB devices, such as USB flash drives, digital cameras, mice or keyboards, to >be attached to them. Use of USB OTG allows those devices to switch back and forth between the roles of host and device. A mobile phone >may read from removable media as the host device, but present itself as a USB Mass Storage Device when connected to a host computer.

So in short, we are using pin 4, or the ID, as a way to tell our Muse headset to play host to our new electrode. 

#### Soldering

These pins are small so soldering is tight. There may be a better method, but below is how I did it. Additionally, if you purchased the 10-piece Micro USB kit, I recommend practicing on a couple pins with some old wire.

  * Consider using 60/40 Flux Core Solder Lead/Tin solder which is easier to use in almost all cases. 
  * Wear a disposable respirator with at least a P100 rating (3M P100 Disposable Respirators on Amazon are under $15 per mask) to protect your lungs from the metal infused smoke that comes off of hot solder. A P100 rating will filter out 99.97% of pollutants, dust, and solvents from the air. 
  
1. Add solder to each of your individual wires first. 

![Soldering each wire individually](https://cdn.hackaday.io/images/100741541190829176.jpg)

2. Then, touch the wire to the corresponding pad. And touch a hot, fine tip, soldering iron to the wire so the solder in the wire can heat up and adhere to the pad.

![Touching wire to corresponding pad](https://cdn.hackaday.io/images/4499701541190975151.jpg)

And we should end up something like the following photo below.

![Micro USB with solder on pin 4](https://cdn.hackaday.io/images/1291441541311088787.jpg)

Below is a photo of a blunder I made where my hand slipped and I got solder on pin 4 and pin 5 - not good, so I cut close to the wire, exposed some more wire and gave it another go.

![Blunder example](https://cdn.hackaday.io/images/3728191541191043299.jpg)

### Step 4: Heat Shrink and Plastic Encasing
Once soldered together, wrap the heat shrink around the Micro USB so it sticks out a little when clipping together the plastic encasing. 

![Heat shrink](https://cdn.hackaday.io/images/2937751541191220582.jpg)

Then use the soldering iron for shrinking the heat shrink (I'm not sure if this is necessary, but it looks nice), and finally clip the plastic encasing pieces together.

![Plastic encasing](https://cdn.hackaday.io/images/1319401541191256499.jpg)

### Step 5: Hook & Loop
Next, we’ll make a simple strap that will help us hold our new electrode in place on our heads!

Take your roll of hook and loop and cut about 20 inches off. Find the middle by folding it in half and mark it by using a hole punch. 

Note: I used ~20 inches because I wanted to play around with it, but 12-15 inches will probably look more "fitted."

Not shown below, but peel off your square hook & loops and stick those onto the sides of the Muse headset for the strip you are about to cut to "hook" onto (see final image with the white squares on the side of the Muse headset). 

![Role of hook and loop](https://cdn.hackaday.io/images/6253021541191496498.jpg)

![Hole punch hook and loop](https://cdn.hackaday.io/images/3516981541191513833.jpg)

Kind of hard to tell, but the photo below has the electrode inserted in the middle hole ( you might have to cut a little on the sides of the holes with some scissors to get the electrode to fit snug). 

Wrap the excess wire in the unused holes so it's tucked away.

![Loop electrode through the holes in the hook and loop](https://cdn.hackaday.io/images/3293581541191610902.jpg)

### Step 6: Attach Hook & Loop To Muse
With the 10-20 placement in mind, Oz (directly back of the head) or Cz (directly top of the head) are configurable with this setup, but in theory you could get weird, make more holes, and configure accordingly. Go wild.

![Loop electrode through the holes in the hook and loop](https://cdn.hackaday.io/images/6533301541191758537.jpg)

### Step 7: Connect, Test / Muse-LSL
Not going to go into the details of how to connect your headset to your computer as there are way better tutorials out there for that, like [this](https://github.com/NeuroTechX/bci-workshop/blob/master/INSTRUCTIONS.md), or [this](https://github.com/kowalej/BlueMuse) one for Windows. 

The important thing is that the "Right Aux" channel should correspond to the extra electrode that we've constructed. Once you've applied it firmly to the head with the strap, ensured connectivity through hair, and let things settle for a while, it should display a signal that looks similar to the four main Muse channels.

![Loop electrode through the holes in the hook and loop](https://cdn.hackaday.io/images/5829161541311974330.PNG)

Congrats! You've extended the capabilities of a Muse headset and are able to implement more of the classic EEG BCI paradigms such as [P300](https://eeg-notebooks.readthedocs.io/en/latest/visual_p300.html) and [SSVEP](https://eeg-notebooks.readthedocs.io/en/latest/ssvep.html)!

Have fun! And if you have any questions, comments or suggestions on the above steps, please feel free to reach out.
