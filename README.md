# Festival Mesh Networking
Guide to Meshtastic setup for Festivals/Events

## Description
Finding your friends at festivals without phone signal is HARD, [Meshtastic](https://meshcore.co.uk) changes all that. Think: Off-Grid WhatsApp that actually works!

If your festival/event has poor mobile phone signal and you struggle to find your friends, you can keep in touch by using [Meshtastic](https://meshtastic.org/). This guide helps you configure and operate your off-grid mesh communications network, specifically with devices and settings that have been battle tested at festivals and events. The following has been successfully tested with over 100 nodes at the beautiful Shambala festival (UK), where phone signal is non-existent yet Metastatic works flawlessly.

### Community run (very unofficial)
- The official [Meshtastic Documentation](https://meshtastic.org/docs/introduction) is excellent however, it can go into a lot of depth and is very broad (to cater to many use cases). This is a quick-start guide if you just want to get you and your friends up and running quickly for an event/festival.
- This is a place to co-ordinate, share configuration, ask the community for help.
- See GitHub Discussions to ask (and kindly answer) questions. 
- Your contributions are very welcome here!

## What you need
- Companion device | Cost: circa £30-£40 each
Each person in your group will need their own companion device paired with the Meshtasctic app on their phone.
The two best companion devices to get are:
- [Seeed X1 Tracker](https://wiki.seeedstudio.com/meshtracker_x1_intro/)
- [Rak Wizmesh Tag](https://store.rakwireless.com/products/wismesh-tag-meshtastic-gps-lora-tracker-ip66)

## App (free)
You connect your phone to your companion device over Bluetooth. 
You use the messaging function from the Meshtastic app on your phone.
- [Meshtastic from Apple App Store](https://apps.apple.com/gb/app/meshtastic/id1586432531)
- [Meshtastic from Google Play Store](https://play.google.com/store/apps/details?id=com.geeksville.mesh)
- [Meshtastic from F-Droid App Store](https://f-droid.org/en/packages/com.geeksville.mesh)

## Shared Configuration
Please kindly configure your nodes responsibly and with consideration... If you configure them incorrectly, you will negatively affect everybody's experience, including your own.

### Coordinate on your mesh settings
For the most effective mesh, everyone uses the same modem/radio settings at the event. The intention of this repo is to give everyone a reference for settings/configuration so that we all help each other's mesh out (one big happy mesh family). Messages only get repeated by other Meshtastic devices if you're all using the same LoRa modem / Radio settings (Eg, same region, same frequency slot, same speed etc.  See more [here](https://meshtastic.org/docs/configuration/tips/#rebroadcast-public-traffic).

### Device Roles
- CLIENT: For almost ALL nodes.
- CLIENT_BASE: for nodes on top of your camper van / tent / venue.
###ROUTER/REPEATER mode...
- [Avoid ROUTER/REPEATER mode](https://meshtastic.org/docs/configuration/tips/#avoid-routerand-repeater)
- ONLY for EXCEPTIONALLY well-sited nodes (eg: Nodes 20+ metres up, central, on a TALL mast / in a TALL tree).
- Too many (or poorly placed) ROUTER nodes will cause network issues. Only use ROUTER/REPEATER mode if you know what you are doing.
- If at Shambala Festival (UK) - Router nodes have already been placed, you don't need them here.
### All other roles
- Ignore them, they aren't relevant for festivals/events.

### Overcoming Network Congestion
100+ nodes is approaching the limit of the default "LongFast" preset. At festivals/events, you should expect to a high density of nodes in a small geographic area. So with that, range is less of a concern and congestion becomes the main concern. Use the following settings to overcome the limitations of the default "LongFast" preset.

### For the highest certainty that your messages will be delivered at your event use these settings...
***(If the setting isn't in this list, it should be left as the default setting)
- Country/Region: Europe 868mhz (For UK / Europe)
- Preset: Medium Range - Fast
  (MediumFast can handle far more nodes than the default LongFast before becoming congested in a dense network, see: [Presets](https://meshtastic.org/docs/overview/radio-settings/#presets))
- Rebroadcast Mode: Core Portnums Only
- Frequency Slot: 0
- Number of Hops: 3
- Ignore MQTT: ON
- OK to MQTT: OFF
- Transmit Enabled: ON
- Coding Rate: (Use Preset Default)
- RX Boosted Gain: OFF (Uses more battery when on. Not required in a dense network at events)
- User config: Set your 'Long Name' and 'Short Name' so everyone knows who you are in your channel
- Position config...
     (Please don't be tempted to set these any lower as it can easily flood and overwhelm the network)
     Smart Position: ON
     Minimum Interval: 5 Mins
     Minimum Distance: 30 Metres
     Device GPS Update Interval: 5 Mins

## Channel Setup
Meshtastic is multi-channel (In the same way you might have multiple WhatsApp groups)
- A public channel (eg: everyone within range)
- A private channel (eg: a private WhatsApp group between only you and your friends)
- Multiple private channels to keep different groups of friends separate.

### Easiest Channel Setup
(A single private channel, no public channel):
- Delete the default channel (This has no encryption, so intentionally, location sharing doesn't work)
- Add a new channel, name it, enable encryption (key size: 256-bit). (This will be your primary, private channel. Location sharing works)
- (Optional): On your new private, primary channel, enable [`Position Requests` and `Precise Location`](https://meshtastic.org/docs/configuration/radio/channels/#position-precision)
- MQTT: Uplink & Downlink: OFF
- Share your channel with your friends. (`SETTINGS` > `SHARE QR CODE`)

### Multi-Channel Setup
(Public channel and one (or more) private channels):
- See official manual [here](https://meshtastic.org/docs/configuration/tips/#sharing-location-on-a-private-secondary-channel)

## Future additions
To-Do / Contributions welcome...

- Map overlays
Each year the festival map changes with the new venue layout. We must obtain the new festival map and overlay it to the correct latitude/longitude within the Meshtastic app - doing so enables you to see the location of your friends, relative to the festival layout. This assumes you are using one of the companion devices that include GPS/GNSS functionality (see recommended devices above).

- Alternative mesh technologies
In the future this repo may also include information about using MeshCore, which is an alternative to Meshtastic.

- Coordinate on ROUTER/REPEATER locations. 

- Contact festival organisers to request placing ROUTER node on one of the festival's existing masts.
