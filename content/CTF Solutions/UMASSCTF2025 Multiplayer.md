---
title: UMASSCTF2025 Multiplayer
draft: false
tags:
  - OSINT
---


## Problem

You and a friend want to play Fireboy and Watergirl in the Forest Temple, but you both live quite far away. You both want to meet up roughly halfway by distance, you want to meet at a place that has public computers, and you want to meet up at a place that shares the name of the street where you both live. What’s the address of where that could be?

Flag format: UMASS{Address as on Google Maps}, e.g. UMASS{650 N Pleasant St, Amherst, MA 01003} for the Integrative Learning Center at UMass.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXftpfdwM5gyCfqDNPyHwAaRG_-w9HfJmdwozcvrQ5Z1AdxTT3dKt08bLZtLsuazoxVShF3OXv9CKHa1T_HtLDXEFiyqmZFwTU2kChrSimd9Ta8_u17H6q3w68SyI8aZ0LJhDEBC?key=40mM8Y3GhBkfW4HC1QNQrkFC)

Above is image number 1 called: multiplayer 1

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeYHhY4ZqQjHR3_i4tKED9Uk7Aq2p41o90gjFUIFHxk5fjOWZPXowytYSMM1nNUvWkaV653Y_B-8750QW-BzAYGeaS6nWYBu9x5PTygCDcEz9NovYWDVXRbdSiZW3hymglps0ay?key=40mM8Y3GhBkfW4HC1QNQrkFC)

Above is image number two called: multiplayer 2

  

## Solution

### Step 1: Locating the Images

The first step is to determine where these panoramic images are. When observing multiplayer1, the trash can holds some critical information. There is a street sign reading Pennsylvania and Norfolk. Another critical piece of information is found on the green trash bin. Below is a close up of the trash can.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd-vXYQgmm_ABueZildJq2wNmpnXjFrloc3KhqR6Nwr7d0Mqy2aV9X68FsnHZLqrwLdki1zFU82dN4ahqrukjIO4YTrF9BuFGb6-42CWhA0QXkt9vzc0TR8fc2i3YdTs4-WpnhA?key=40mM8Y3GhBkfW4HC1QNQrkFC)

The text says “Henrico County Reuse Collection”. This is probably the county or city where this street is located. I looked up “Pennsylvania Avenue Henrico” and got sent to Henrico, Virginia near Richmond.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTGFBqy45EKwkkSqtDusoR-yo-soLoHaFNF_oCl4HIDKcNfIwFTlIfERzRA-r8YSZ0IuWzeEGNSgQtSclwD0HyWrYvosr7JGjqWRhcH1aZNCR_nKkKQdBVxbjtdelOxKUsSfgd6Q?key=40mM8Y3GhBkfW4HC1QNQrkFC)

This is definitely the location of the first image. Here is a link to the [location](https://www.google.com/maps/place/37%C2%B038'59.2%22N+77%C2%B027'50.2%22W/@37.649778,-77.463945,17z/data=!3m1!4b1!4m4!3m3!8m2!3d37.649778!4d-77.463945?entry=ttu&g_ep=EgoyMDI1MDQyMi4wIKXMDSoJLDEwMjExNDU1SAFQAw%3D%3D). Feel free to look in Google Map’s street view.

For the second image, the main observations are the street names Pennsylvania and 19th street. In addition, there is a sign about a snow emergency route indicating that the location is somewhere cold during the winter. I scoured the map looking up “Pennsylvania Avenue and 19th Street” and found Allentown, Pennsylvania. The [street view](https://www.google.com/maps/@40.6130276,-75.5048425,3a,75y,188.5h,76.82t/data=!3m7!1e1!3m5!1sUlfcq5EKgG2V9LRTbLxfnQ!2e0!6shttps:%2F%2Fstreetviewpixels-pa.googleapis.com%2Fv1%2Fthumbnail%3Fcb_client%3Dmaps_sv.tactile%26w%3D900%26h%3D600%26pitch%3D13.180000000000007%26panoid%3DUlfcq5EKgG2V9LRTbLxfnQ%26yaw%3D188.5!7i16384!8i8192?entry=ttu&g_ep=EgoyMDI1MDQyMi4wIKXMDSoJLDEwMjExNDU1SAFQAw%3D%3D) matches the second image, confirming the location.

### Step 2: Finding the Midpoint

The problem states that the partners want to roughly meet at the halfway point. On google maps, I set a route from multiplayer1’s location in Virginia to multiplayer2’s location in Pennsylvania. Below is the [route](https://www.google.com/maps/dir/1901+Pennsylvania+St,+Allentown,+PA+18104/37.649778,-77.463945/@39.129412,-77.7197707,8z/data=!3m1!4b1!4m9!4m8!1m5!1m1!1s0x89c439f2af51943b:0x1d61d1d5c8c2a4e8!2m2!1d-75.5047795!2d40.6130528!1m0!3e0?entry=ttu&g_ep=EgoyMDI1MDQyMi4wIKXMDSoJLDEwMjExNDU1SAFQAw%3D%3D).


![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXffh6wWV7awyJ0MYxuegvEfdWkS7uIbIElEnT2KyS5sd_PYQKCYSM-x4hknMk70HSiv09ZaTkqPIq4QsUFV1i_Oy3oz1jO3ywaBhczJyQ1Hwq1CaCtB-2v70JSDILNlVcEAFrdq6w?key=40mM8Y3GhBkfW4HC1QNQrkFC)

The midpoint area is 145 miles, which is in Baltimore! You can find this by visiting the [route](https://www.google.com/maps/dir/1901+Pennsylvania+St,+Allentown,+PA+18104/37.649778,-77.463945/@39.129412,-77.7197707,8z/data=!3m1!4b1!4m9!4m8!1m5!1m1!1s0x89c439f2af51943b:0x1d61d1d5c8c2a4e8!2m2!1d-75.5047795!2d40.6130528!1m0!3e0?entry=ttu&g_ep=EgoyMDI1MDQyMi4wIKXMDSoJLDEwMjExNDU1SAFQAw%3D%3D) link, dragging your mouse over the blue line and finding the distance number roughly half of 285, which is the distance of the journey.

### Step 3: The final location

The last part of the second sentence is crucial to understand.

“you want to meet at a place that has public computers, and you want to meet up at a place **that shares the name of the street where you both live**.”

Both images had the street Pennsylvania meaning that they both live on Pennsylvania Street. Therefore, the place has to have Pennsylvania in its name. A guess I took is that libraries almost always have public computers so I looked up “Pennsylvania Library in Baltimore” in Google Maps and found [this](https://www.google.com/maps/place/Enoch+Pratt+Free+Library+-+Pennsylvania+Avenue+Branch/@39.3099198,-76.6446532,17z/data=!3m1!4b1!4m6!3m5!1s0x89c8036f29dec84f:0xc645cdae7ec81e1c!8m2!3d39.3099157!4d-76.6420729!16s%2Fm%2F042z7h5?entry=ttu&g_ep=EgoyMDI1MDQyMi4wIKXMDSoJLDEwMjExNDU1SAFQAw%3D%3D).

I copied the address, added the flag syntax around it and the solved the challenge

`UMASS{1531 W North Ave, Baltimore, MD 21217}`