# NorthWest Florida Mesh Configuration Guide (Work In Progress)

## Information
- **Last updated:** Feb 27, 2026  
- **Applies to:** MeshCore **v1.13.0**  
- **Discord:** Emerald Coast Mesh — https://discord.gg/yQMvhzMgHY  
- **Coverage area:** Escambia, Santa Rosa, Okaloosa, and Walton Counties  

---

## Purpose
This guide helps new users configure their radios to match the **Emerald Coast** mesh settings so devices can discover each other and communicate reliably.

---

## Table of Contents
- [Purpose](#purpose)
- [Quick Start](#quick-start)
- [Required Local Settings](#required-local-settings)
- [Public Info](#public-info-all-devices)
- [Advert Intervals](#advert-intervals-repeater--room-server-only)
- [App Usage](#ios--android--web-app-usage)
- [Contacts](#contacts-companion)
- [Repeat Mode](#companion-repeat-mode-advanced-️)
- [Troubleshooting](#troubleshooting-common-issues)
## Quick Start

---

### Quick Start (Companion / Personal Node)
1. **Set Preset:** USA/Canada
2. **Change Coding Rate to 8** 
4. **Set your device name**
5. **Discover Repeaters** **Tools → Discover Nearby Nodes**
6. **Send a message to the Public room**

### Quick Start (Repeater / Room Server)
1. **Connect to newly flashed repeater over USB**
1. **Set Preset:** USA/Canada
2. **Change Coding Rate to 8** 
3. **Set Advert Intervals** - 60 Min / 3 Hour
4. Verify discovery via **Tools → Discover Nearby Nodes** from a companion

---

## Device Types and What They Do
Some menu items only appear on companions, repeaters, or room servers.

- **Companion**  
  The device that connects to your phone or computer via **Bluetooth/USB**.  
  - Companions **do not re-broadcast** received messages by default (unlike Meshtastic).  
  - Companions **do not auto-advertise** by default to reduce congestion.

- **Repeater**  
  A dedicated node that **forwards** companion messages, telemetry, and management traffic across the mesh. These are typically a stationary node with good line of sight, often solar powered paired with low power modules.

- **Room Server**  
  A device that acts like a **chat room / bulletin board**, storing up to **32** messages. Useful for leaving messages when users are not connected or are out of range.  
  - A room server can also behave like a repeater when enabled via **CLI**, but it is not advertised as a repeater.  
  - **Best practice:** keep room servers single-purpose unless you’re operating infrastructure and understand the tradeoffs.

---

## Required Local Settings

### Radio Settings (All Devices) ✅ Required
1. Press the **gear icon** (upper right)  
2. Find **Choose Preset**  
3. Select **USA/Canada**  
4. Set the radio values below:

**Emerald Coast RF Profile (Required)**

| Setting | Value |
|---|---|
| Frequency | **910.525 MHz** |
| Bandwidth | **62.5 kHz** |
| Spreading Factor | **7** |
| Coding Rate | **8** |
| Transmit Power | **22 dBm** |

**Note on transmit power (SX1262):**  
The LoRa transceiver (SX1262) has a **max TX power of 22 dBm**. If your device has an embedded amplifier, the additional gain is not shown in the app. Setting **22 dBm** should max the radio’s configured output, but the real radiated power can be higher depending on hardware.

### Defaults and Coding Rate ⭐ Recommended (for now)
Most settings can remain at defaults — the key local recommendation is **Coding Rate = 8**.

Increasing Coding Rate from **5 → 8** applies additional error correction to improve long-range links and resist noise, at the cost of data speed. If the region becomes saturated with devices later, we may reduce Coding Rate to limit congestion.

**Compatibility note:** It may be possible for devices to communicate when Coding Rate differs, but **best practice is to match CR=8** for consistent reliability across the mesh.

### Companion Repeat Mode (leave OFF) ⚠️ Advanced
**Leave Companion Repeat Mode OFF** unless you are coordinating a Meshtastic-style, ad-hoc operation (details in the Repeat Mode section).

---

## Public Info (All Devices)

### Node Naming ⭐ Recommended
You will probably want to change the name of your companion device. This is optional but recommended. Use a prefix so others can identify which devices you own.

Examples:
- 🟢 XXXX (emoji prefix)
- GBXXXX (Discord username initials)
- PNS_XXXX (location)
- _WPR_XXXX (callsign)

Tip: Keep names short and readable. If your community starts standardizing naming later, you can update this section with the official convention.

---

## Advert Intervals (Repeater + Room Server Only)

### What is an “Advert”?
An **advert** is a periodic broadcast of a node’s public info so other users can discover it.

Non-companion devices can automatically advertise their information to the mesh. These values are recommended while our mesh is still growing so repeaters and room servers are easier to discover.

- **Zero Hop adverts**: only reach nodes in direct range; they **do not repeat**.  
- **Flood adverts**: propagate through repeaters across the mesh.

In very dense areas, some communities recommend flood adverts at **24 hours or more**. We’re not at that density yet, so these lower intervals are fine for now and can be increased later.

### Recommended Advert Settings ⭐ Recommended
| Advert type | Interval |
|---|---|
| Auto Advert (Zero Hop) | **60 minutes** |
| Auto Advert (Flood) | **3 hours** |

---

## iOS / Android / Web App Usage

### Connecting
1. Press **Bluetooth Connect**  
2. Your MeshCore radio should appear if it is powered on and not connected to another device.  
3. For initial pairing:  
   - Devices with screens display a **6-digit** code on the main screen.  
   - If you don’t see it, press the **user button** to cycle screens.  
   - Devices without displays often use **123456** (common default).  
4. If you get a red warning message after first connect:  
   - Close the MeshCore app completely  
   - Re-launch it  
   - The radio should connect and begin syncing

> Replace the line below with your actual image path if publishing on GitHub:
>
> `![Bluetooth Connect screen](path-or-url-to-image.png)`

---

## More Options Menu (⋮ / “kebab menu”)

### Tools
- **Tools → Discover Nearby Nodes**  
  Sends an advert and listens for responding repeaters or sensors.  
  ✅ **Recommended first step** after you configure your device.

- **Internet Map**  
  Shows nodes whose details have been uploaded.  
  ⭐ Recommended to finish configuration—especially **location settings**—before sharing.

---

## Contacts (Companion)

### Adding contacts (⋮ → Add Contact)
This allows manual contact adding, rather than waiting for an advert. There are multiple ways to import:

- **Manual**  
  Choose contact type (Chat, Repeater, Room Server, or Sensor), then enter the name and public key.

- **Import from Clipboard Link** (most common for texting friends)  
  Copy the provided URL; the import button reads it from your clipboard and adds the contact.  
  Can import repeaters, room servers, companions, and private channels.

- **Scan a QR Code**  
  Great for in-person meetups and adding private channels.

- **Internet Map**  
  Find a repeater and add it to contacts before you hear an advert.  
  Note: this doesn’t make it work unless you’re actually in range—**Discover Nearby Nodes** is often the better strategy.

### Managing contacts ⭐ Recommended tips
- In the **Contacts tab** (lower left), you can search, filter, and sort your contacts.
- You can set a **custom name** for someone else’s node:  
  open their **⋮** → **Details** → edit name with the **pencil** icon.  
  Only you can see your custom names.

### Auto-add behavior (optional)
If you do not want all nodes/devices to be auto-added:
1. Go to **Device Settings → Contact Settings**
2. Disable **Auto Add All**
3. Select which device types you want auto-added

To manually add contacts:
- Use **⋮ → Discover contacts**
- Add the ones you want from devices you’ve received an advert from

---

## Messaging
- Users can send messages to the **Public Channel** where all companions receive a copy.  
- **Private channels** can be created to provide an encrypted channel for multiple companions to join.  
- **Direct messaging** is supported, but both devices must have each other added as a contact.  
  Blind messaging does not work.

---

## Companion Repeat Mode (Advanced) ⚠️
**MeshCore v1.13.0+**

By default, MeshCore companions **do not relay** other users’ traffic. This reduces congestion and relies on dedicated repeaters/room servers for forwarding.

**Repeat Mode** makes a companion behave more like Meshtastic’s flooding strategy (more devices relaying packets), which can help in temporary off-grid situations but can also increase congestion and duplicates in a fixed infrastructure mesh.

MeshCore’s standard routing architecture is optimized for fixed-node meshes and supports up to **64 hops** (compared to **7** on Meshtastic), which is one reason the default behavior avoids flooding from every handheld.

### Repeat Mode requirements (must coordinate)
If you enable companion Repeat Mode:
- You must use **918 MHz** when Repeat Mode is enabled  
- You must **type it in** and apply the settings  
- You must coordinate and match settings with the other users you want to mesh with  

> ⚠️ This is not intended for everyday use on the Emerald Coast mesh profile unless the community explicitly standardizes it.

---

## Join Test (Verify Your Setup)
After saving settings and rebooting:

### Basic checks ✅
- You can connect in the app without errors (or errors clear after an app restart)
- Run **Tools → Discover Nearby Nodes**
- You see at least one nearby repeater/room server (if you’re in range)
- Send a test message in the Public Channel and confirm someone receives/replies

---

## Troubleshooting (Common Issues)

### “I can’t connect / radio won’t pair”
- Ensure the radio is not connected to another phone/computer
- Try closing the app completely and relaunching
- Confirm pairing code screen (cycle device screens with the user button)
- For no-display devices, try **123456** (if your hardware uses that default)

### “Discover Nearby Nodes finds nothing”
- Re-check the **Required RF Profile** values (frequency/bandwidth/SF/CR)
- Move outdoors or near a window
- Verify you saved settings and the radio rebooted

### “I can see nodes but DMs don’t work”
- Both devices must have each other added as contacts
- Confirm you’re messaging the correct contact (custom names help)

---

## Changelog
| Date | Version | Changes |
|---|---|---|
| Feb 27, 2026 | Draft | Initial draft formatting + local settings |
