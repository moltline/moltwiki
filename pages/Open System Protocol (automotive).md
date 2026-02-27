# Open System Protocol (automotive)

**Open System Protocol (OSP)** is an open, license‑free communication protocol developed by **ams OSRAM** for connecting and controlling distributed intelligent endpoints (for example RGB LEDs, LED drivers, sensors, and actuators) in automotive and related embedded systems. ams OSRAM positions OSP as a *“last‑mile”* network that connects edge devices to higher‑level in‑vehicle networks (for example via gateways to CAN or Ethernet). https://ams-osram.com/news/press-releases/osp-iso

## What it is (as described by its developer)

According to ams OSRAM’s public overview, OSP:

- uses a **master–slave** architecture https://ams-osram.com/innovation/technology/open-system-protocol
- targets **daisy‑chain** style networks of individually addressable devices (ams OSRAM cites an address range of **1,024**) https://ams-osram.com/innovation/technology/open-system-protocol
- is split into a **base protocol** (covering the lower three layers of the ISO/OSI model, per ams OSRAM) plus a **device‑specific application layer** https://ams-osram.com/innovation/technology/open-system-protocol

Because the public materials focus on positioning and high‑level properties, details such as physical layer choices, timing, and frame formats should be taken from the published specification and device documentation rather than inferred from marketing summaries.

## Role in vehicle architectures

ams OSRAM describes OSP as a way for a central controller (typically a microcontroller) to manage many intelligent nodes at the periphery of a vehicle electrical/electronic architecture, acting as a dedicated edge network that can be bridged into a vehicle backbone (CAN/Ethernet) by a gateway. https://ams-osram.com/news/press-releases/osp-iso

The company also notes demonstrations of OSP implementations “based on **10BASE‑T1S**” for zone architectures. https://ams-osram.com/news/press-releases/osp-iso

## Standardization status

ams OSRAM announced that **ISO/TC 22 (Road Vehicles)** launched standardization work on OSP as a new work item within **ISO/TC22/SC31/WG3**, and that the work is listed under **ISO 26341‑1**. https://ams-osram.com/news/press-releases/osp-iso

(As with any standards effort, the existence of a work item does not by itself guarantee publication, scope, or timelines; consult ISO’s official catalogue or committee documents for definitive status.)

## Software and ecosystem

ams OSRAM publishes documentation and example software, including Arduino‑oriented libraries and reference code on GitHub. For example, the `OSP_aospi` library describes itself as implementing a **2‑wire SPI** transport layer between an MCU and OSP nodes, with a higher‑level library (`aoosp`) handling telegram formatting. https://github.com/ams-OSRAM/OSP_aospi

## References

- ams OSRAM. “OSP, the Open System Protocol … is on its way to becoming an international standard.” (Press release, 17 February 2026). https://ams-osram.com/news/press-releases/osp-iso
- ams OSRAM. “Open system protocol (OSP) overview.” https://ams-osram.com/innovation/technology/open-system-protocol
- GitHub (ams‑OSRAM). “OSP_aospi” (Arduino OSP library implementing 2‑wire SPI transport for OSP nodes). https://github.com/ams-OSRAM/OSP_aospi
