---
title: Buying an X-Wing
excerpt: In which I converse with an imaginary spaceship distributor
header:
  overlay_image: header.png
---

I've been working on an RF circuit board at work.
For one particular stage of the board, I want a variable gain amplifier that works from dc to 450 MHz, has differential output, and digitally programmable variable gain.
To find a part like that, you have to read a lot of spec sheets, and once you've read enough spec sheets, they all start to sound kinda the same.
Here's an excerpt from the ADL5205's spec sheet:

> The ADL5205 is a digitally controlled, wide bandwidth, variable gain dual amplifier (DGA) that provides precise gain control, high output third order intercept (OIP3) and near constant noise figure for the first 12 dB of attenuation.
>
> ...
>
> Fabricated on the Analog Devices, Inc., high speed, silicon germanium (SiGe) complementary BiCMOS process, the ADL5205 provides precise gain adjustment capabilities with good distortion performance.
>
> ...
>
> The quiescent current of the ADL5205 is typically 175 mA for high performance mode and 135 mA for
low power mode.

You realize, after reading enough of these things, that they all follow the same pattern.
They first tell you the part number and give a list of all the most important features that make it awesome and should convince you to buy it.
Then there's usually some reminder about who the manufacturer is (in case you already forgot and for some reason care), along with a brief list of secondary features.
Then, at the end, there's always a statement about power requirements, often combined with a statement about what you need to do to maximize the device's performance.
Note that word "performance"; it's always there.

After two day of reading spec sheets, I came home in the evening and felt like playing one of my favorite Nintendo games, *Rogue Squardon 2*.
Before each mission, you get to run around a starship hangar and choose your craft.
Seeing all the different ships, A-Wing, X-Wing, Y-Wing, TIE fighter<sup>`[1]`</sup>, and even the Millenium Falcon in the hangar really adds to the feel of the game.
There's even a little feature where you can listen to the game's narrator give a technical description of each ship.

Perhaps you see where this is going.

Having just come off of spec sheet safari, I couldn't help but notice that the ship descriptions in a galaxy far, far away follow the same template as our IC spec sheets.
Here's an example for the X-Wing.

> The Incon T-65 X-Wing is the fighter that killed the Death Star. An almost perfect balance of speed, maneuverability, and defensive shields make this the fighter of choice for Rogue Squadron...

See that?
We got the manufacturer, the part number, and a list of the important performance metrics right at the beginning.
Here's the rest

> ...except when the mission profile disallows it. In addition to four blaster canons, the X-Wing can carry a number of Proton Torpedoes. It’s powered by four fusial thrust engines, and requires an onboard astro-mech droid for peak performance.

Extra features, power, and a warning about needing an astromech droid for peak *performance*.
There we go, a long time ago in a galaxy far, far away, buying an illegally manufactured starfighter must have been a lot like buying an integrated circuit chip in our galaxy today.
As usual, thinking about all of this started in an imaginary conversation in my head:

**Imaginary Galactic Ship Manufacturing Inc. (IGSMI):** ...so as you can see, the X-Wing is the fighter of choice for your battle application.

**Me:** Ok ok, I can see the X-Wing is awesome. How much does it cost?

**IGSMI:** The X-Wing is priced competitively to give you the edge against your imperial competition.

**Me:** Yeah so how much?

**IGSMI:** For pricing information, contact a vendor in a star system near you.

**Me:** Oh for... ok fine. Who's the vendor for my region?

**IGSMI:** Please create an account through our secure online system to find distributors.

**Me:** *groan* Fine. Done. Now, who's the vendor for the [Sullust system](http://starwars.wikia.com/wiki/Sullust)?

**IGSMI:** That would be Incom Inc. Please contact them for pricing and availability.

**Me:** Can you give me their subspace holochat number?

**IGSMI:** I don't have that information. Please see their website for contact information.

**Me:** Their website only lists a phone and fax number. Who uses fax in the age of holochat? Whatever. *::dials phone::* Hi, I'd like to ask about X-Wing pricing.

**Incom sales rep:** Sure I can help you with that. Can I have your name, address, company, holochat number, phone number, fax number, social security number, criminal record, and a thumbprint please?

**Me:** Uh, I already have an account with you guys.

**Incom sales rep:** Ok log in to our secure system.

**Me:** I forgot the password because I never wanted to make an account in the first place.

**Incom sales rep:** That's ok, give me your username and we'll send you your password in plain text.

**Me:** I thought this was a *secure* system!

**Incom sales rep:** It is! We never tell anyone else your password.

**Me:** Look, I'm just trying to buy an X-Wing. It's for a hobby project. I just need one. Can I just order one right now through you? I can pay with a credit card.

**Incom sales rep:** Our minimum order quantity is ten thousand. Are you sure you don't need more?

**Me:** Screw this. I'm joining the Empire.

That was left out of the films, I guess.

`[1]`: Yeah, you can get a TIE fighter. Look online for how to do it. The TIE is kind of crappy though because a couple hits and your a ball of flame.
