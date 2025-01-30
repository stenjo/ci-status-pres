---
theme: apple-basic
layout: intro-image
image: 'images/frontcover.jpeg'
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
layout: intro
image: 'images/StenOttoJohnsen_6879.jpg'

---

# About me

## Sten Johnsen


---

# Background

ABB Robotics

test-rack

e2e tests heavy and not run on pr commit


---

# Stuff you need


---

# Programming the RGB controller

Soldering wires and wireless

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
image: 'images/raspi-screendump.png'
---

---

# Setting up an MQTT Broker


---

# Mounting column in the team-room


---

# Setting up workflow calls

---
layout: 3-images
imageTopRight: 'images/IMG_2446.jpg'
imageLeft: 'images/rgb_wires.jpeg'
imageBottomRight: 'images/serial-adapter.jpeg'

---

---

