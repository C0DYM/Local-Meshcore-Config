# NorthWest Florida Mesh Configuration Guide (In Work)

## Information
- Last updated: [FEB 27, 2026]
- Applies to: Meshcore 1.13.0
- Discord: Emerald Coast Mesh - https://discord.gg/yQMvhzMgHY
- Locations: Escambia, Santa Rosa, Okaloosa, and Walton Counties

## Purpose

This guide helps new users configure their radios to match the Emerald Coast mesh network settings so devices can discover others and communicate reliably. 

## Configuration

Certain menu items are only available on either companions or repeaters/room servers. 

- **Companion**: This is the device that will connect to your phone or computer via bluetooth/usb. Companions do not re-broadcast received messages like Meshtastic does. Companions do not auto-advertize, to reduce potential congestion. 
- **Repeater**: These devices repeat companion messages, telemetry, and management to other devices on the mesh.
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

The only recommended modification is to the Coding Rate. By inreasing from 5 -> 8, additional error corrections are implemented to improve long range connections and resist noise at the cost of data speed. In the future the area may get saturated with devices; This recommendation would change to a lower value to reduce congestion. Devices CAN communicate with eachother when the Coding Rate value is different. Do not Enable Repeat Mode (Only a companion option) unless you do not want to participate in the mesh. More on this below.

### Public Info - All Devices
You will probably want to change the name of your companion device. It is optional but recommended to use some sort of prefix to identify which devices you own. Examples:
- 🟢 XXXX (Emojis)
- GBXXXX (Discord Username Initials)
- PNS_XXXX (Location)
- _WPR_XXXX (Callsign)

### Advert Intervals - Repeater + Room Server Only

Non-Companion devices can automatically advertize their information to other users on the mesh. These values are recommended to be low while our mesh is still growing, which allows repeaters and room servers to be automatically discovered by other nodes. Zero Hop Adverts are the nodes in line of sight of eachother, these messages do not repeat. Flood adverts are sent through every available repeater. In very dense areas, they recommend 24 hours or more. We don't have that problem, and can adjust in the future once the mesh is larger.

- Auto Advert (Zero Hop): 60 Minutes
- Auto Advert (Flood): 3 Hours

# iOS/Android/Web App Usage

### Connecting

### Menu ⋮ 
- Tools -> Discover Nearby Nodes: This will have your compoanion send out an advert and listen for responding repeaters or sensors. This is the recommended first step after configuring your device.
- Internet Map: This will show nodes who's details have been uploaded. It is recommended to finish configuring the devices, particularly the location before sharing.


### Contacts - Companion
- Menu ⋮ -> Add Contact: This allows for manual contact adding, in lieu of waiting for an advert. There are 3 ways to import a contact.
  - Manual: You will need to choose the contact type (Chat, Repeater, Room Server, or Sensor) along with the name and Public Key.
  - Import from Clipboard Link: Most common method for sharing over text messages to friends. Copy the URL provided, and the import button will paste it from your clipboard and add the contact. You can import repeaters, room servers, companions, and private channels.
   - Scan a QR Code: Exactly what it sounds like. Good for in person meetups, for adding private channels.
   - Internet Map: Check out the area and click on a repeater, you can add it to your contacts before hearing an advert. This won't make it work unless you're in range, which a "Discover Nearby Nodes" may be a better strategy.
- In the contacts tab (lower left), you can search, filter, and sort your contacts.
- You can set a custom name for someone else's contact by clicking on their ⋮ icon, go to details, and edit their name using the pencil icon. You can make a completely custom name, or take their repeater name and add additional information (like discord username, callsign, etc) to it. Only you can see your custom node names.
- If you do not want all nodes and devices to be auto-added, go to your device settings -> contact settings. disable "Auto Add All", and select the types you wish. To manually add contacts, you must go to ⋮ -> Discover contacts, and add the ones you wish to your contact list. This list is comprised of devices you have received an advert from.

### Messaging

- Users can send messages to the "Public Channel" where all companions will receive a copy. 
- Private channels can be greated to provide an encrypted channel for multiple companions to join.
- Direct messaging to devices are supported, but both devices must have the other added as a contact. Blind messaging does not work.

## Companion Repeat Mode
Released in version 1.13.0, repeat mode changes the main functionality of MeshCore to behave like Meshtastic. By default, Meshcore companions do not repeat any messages. Companions do direct message other companions if within range. Meshtastic uses the flood strategy - All devices repeat all packets, regardless of who they originated from - to enable off grid, no-infrastructure messaging with the best chance of message delivery. In larger, fixed node meshs, this strategy can cause excess congestion, inefficient routing, and multiple copies of messages being received. Meshcore has optomized their standard routing archatecture to allow for up to 64 hops compared to 7 on Meshtastic. 

For those times when you need a Meshtastic like capability, you can enable the companion repeat mode. You will have to utilize 918MHz when this mode is enabled, you must type it in and apply the settings. You must coordinate and match settings with other users for the mesh to work.




