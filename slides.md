---
theme: apple-basic
layout: intro-image
image: '/images/frontcover.jpeg'
title: CI Status indicator

transitions: slide-left, slide-right

mdc: true
---
<div class="absolute top-5">
  <span class="font-700">
    Sten Johnsen: 
    Bouvet One - March 2025
  </span>
</div>

<div class="absolute bottom-10">
  <h1>CI health status column</h1>
  <p>How to build and use a radiant status indicator in the team room</p>
</div>

---
layout: default
transition: slide-up

---

# Sten Johnsen

A tech geek spending his work and spare time figuring out stuff involving electronics and software


- **Bouvet** - Since 2008, currently team-lead and (full-stack) developer
![Sten](/images/StenOttoJohnsen_6879.jpeg) {width=200px margin=30px align=right}

- **Experience** - Graduated 1991 - B.Eng Microelectronic computer systems. Programming since my first real job - never looked back.
  
- **Roles** - Programmer, project manager, program manager, department head, entrepreneur, agile coach and relationship counsellor

- **Trainer** - DevOps certification courses, Agile, Scrum

- **Busy with** - Quality of software and creating high performing teams

---
layout: image-right
image: /images/testrack.webp
---

# Inspiration


ABB Robotics had a policy of backwardds compatibility of their software on all årevious controller designs

test-rack

e2e tests heavy and not run on pr commit

<!--
The story about how they displayed the last committer on the info-screens if the nightly builds and tests failed
-->
---

# End-to-end tests

graph - gihub workflow


---
layout: two-cols
---

# Solution



dagram

Workflow result trigger a light on the status-column

::right::
```mermaid {scale: 0.7, alt: 'Sequence of events'}

flowchart TD
    A[GitHub Workflow] -->|Triggers MQTT Message| B(MQTT Broker at Home 🔒)
    B -->|SSL & Authenticated Message| C[RGB LED Controller 🟢🟡🔴 at office]
    C -->|Subscribes & Sets Light| D{Status}
    
    D -->|Green| E[✅ Success]
    D -->|Yellow| F[⚠️ Running]
    D -->|Red| G[❌ Error]
    
    style B fill:#f9f,stroke:#333,stroke-width:2px
    style C fill:#bbf,stroke:#333,stroke-width:2px
    style D fill:#ff9,stroke:#333,stroke-width:2px
```

<!--
MQTT Broker should be set up at the Bouvet office - available for others as well
-->

---
layout: image-right
image: /images/bom.png

---

# Stuff you need

- Status column (AliExpress, [Item 4000386522400](https://www.aliexpress.com/item/4000386522400.html))
- MagicHome RGB LED Controller (AliExpress, [Item 1005005897407952](https://www.aliexpress.com/item/1005005897407952.html))
- 24V powersupply (Kjell&Co, [Switchet strømadapter 24 V (DC) 24 W](https://www.kjell.com/no/produkter/elektro-og-verktoy/stromadaptrer/acdc-stromadapter/fast-utgangsspenning/switchet-stromadapter-24-v-dc-24-w-p44789) )
- 2 x bolts & nuts for mounting
- MQTT Broker available publicly



---
layout: image-right
image: /images/rgb_wires.jpeg
---

# Programming the RGB controller

The LED RGB controller needs to be reprogrammed because China

To do this we need wires soldered to the board

Connect to a USB->TTL Serial converter and verify you have contact

Note:

- Soldered pads are brittle and comes off easily
- Make sure the `boot` pad is connected to `V33` either directly or via 10K resistor.
- NEVER connect any wire to anything other than `GND` or `V33` unless to serial adapter.


---

# Programming OTA

There is an easier way:
- Download the ota binary from releses page
- Find a linux machine. Raspberry Pi will do
- Open a terminal and start a simple server:
```bash
{
    echo -ne "HTTP/1.0 200 OK\r\nContent-Length: "$(wc -c < OpenBL602_1.17.553_OTA.bin.xz.ota)"\r\n\r\n"
    cat OpenBL602_1.17.553_OTA.bin.xz.ota 
} | nc -l 1111
```

- Power on the RGB controller and connect the linux machine to the wifi `LEDnet_0033xxxxxx` 
- Open a second terminal and enter:
```bash
echo -e "AT+UPURL=http://10.10.123.4:1111/update?version=33_48_20240418_OpenBeken&beta,pierogi"
 | nc -u 10.10.123.3 48899
```

Wait a few minutes, reboot and you should have OpenBeken SW running.

---
layout: image
image: /images/raspi-screendump.png
---

---

# Setting up an MQTT Broker


---
layout: image-left
image: /images/IMG_2469.jpeg

---

# Mounting status-ligths

To fit nicely: 
- Had to create and 3D-print a suitable bracket

![Bracket](/images/mounting-bracket.png)

---

# Setting up workflow calls

---
layout: 3-images
imageTopRight: /images/IMG_2446.jpg
imageLeft: /images/rgb_wires.jpeg
imageBottomRight: /images/serial-adapter.jpeg

---

---

# References


---
layout: fact

---

# Thank you!




## ![Presentation](/images/QR.png) {width=150px margin=30px align=right}
