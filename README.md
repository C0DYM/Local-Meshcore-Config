# NorthWest Florida Mesh Configuration Guide (In Work)

## Information
- Last updated: [2026-02-27]
- Applies to: Meshcore 1.12.0 - 1.13.0
- Discord: Emerald Coast Mesh - https://discord.gg/yQMvhzMgHY

## Purpose

This guide helps new users configure their radios to match the Emerald Coast mesh network settings so devices can discover others and communicate reliably. 

## Configuration

Certain menu items are only available on either companions or repeaters/room servers. 

- **Companion**: This is the device that will connenect to your phone or computer via bluetooth/usb.Companions do not re-broadcast received messages like Meshtastic does. 
- **Repeater**: These devices repeat your companion's message to other devices on the mesh. They have auto-discovery settings not available on other modes.
- **Room Server**: You can flash any device to act as a chat room. It can store up to 32 messages, and is a good way to leave messages for users when they are not connected or out of range. Room Servers can also be repeaters when enabled via CLI - But are not advertized as such and are best suited serving a single purpose. 

### Radio Settings - All Devices
- Press the gear icon in the upper right corner of the screen
- Find the Choose Preset button
- Select USA/Canada
- Change the Radio Settings to the following (press each number to change it):
  - Frequency: 910.525 MHz
  - Bandwidth: 62.5 kHz
  - Spreading Factor: 7
  - **Coding Rate: 8**
  - Do not Enable Repeat Mode, unless you do not want to participate in the mesh

The only recommended modification is to the Coding Rate. By inreasing from 5 -> 8, additional error corrections are implemented to improve long range connections and resist noise at the cost of data speed. In the future the area may get saturated with devices; This recommendation would change to a lower value to reduce congestion. Devices CAN communicate with eachother when the Coding Rate value is different. 

### Public Info - All Devices
You will probably want to change the name of your companion device. It is optional but recommended to use some sort of prefix to identify which devices you own. Examples:
- 🟢 RPTRXX (Emojis)
- GB01 (Discord Username Initials)
- PNSx (Location)
- _WPR_ NodeName (Callsign)

### Advert Intervals - Repeater + Room Server

Non-Companion devices can automatically advertize their information to other users on the mesh. These values are recommended to be low while our mesh is still growing, which allows repeaters and room servers to be automatically discovered by other nodes. Zero Hop Adverts are the nodes in line of sight of eachother, these messages do not repeat. Flood adverts are sent through every available repeater. In very dense areas, they recommend 24 hours or more. We don't have that problem, and can adjust in the future once the mesh is larger.

- Auto Advert (Zero Hop): 60 Minutes
- Auto Advert (Flood): 3 Hours










