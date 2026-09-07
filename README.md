# Festival Mesh Networking Guide (Using Meshtastic)
(Enables off-grid Festival/Event communication between friends)
![Mesh Network Visualization](assets/mesh_network_visualization.png)

## CONTENTS
- [Description](#description)
- [What you need](#what-you-need)
- [Shared-Recommended Configuration](#shared-configuration)
- [Channel Setup](#channel-setup)
- [Future additions](#future-additions)

---

## DESCRIPTION
Finding your friends at festivals without phone signal is HARD, [Meshtastic](https://meshtastic.org/) changes all that. Think: Off-Grid WhatsApp messaging that actually works! Meshtastic networks enable off-grid communication, using inexpensive devices and without traditional mobile phone infrastructure.

This guide helps you configure and operate your off-grid mesh communications network, specifically with devices and settings that have been battle tested at festivals and events. It's been successfully tested with over 100 nodes at the beautiful Shambala festival (UK), where phone signal is non-existent yet Meshtastic works flawlessly.

### This is a community guide (very unofficial)
- The official [Meshtastic Documentation](https://meshtastic.org/docs/introduction) is excellent however, it can go into a lot of depth and is very broad (to cater to many use cases). This is a quick-start guide if you want to get you and your friends up and running quickly for an event/festival without having to wade through and understand the dense official documentation.
- This is a place to co-ordinate, share configuration, ask the community for help.
    See [GitHub Discussions Page](https://github.com/adamsthws/Festival_Mesh_Networking/discussions) to ask (and kindly answer) questions. 

---

## WHAT YOU NEED

#### Companion Device
![Seeed X1 Tracker](assets/seeed_x1_tracker.png)
> Each person in your group will need their own companion device paired with the Meshtastic app on their phone. (Cost: circa £30-£40 each).

Recommended festival companion devices are:
- [Seeed T1000e](https://www.seeedstudio.com/SenseCAP-Card-Tracker-T1000-E-for-Meshtastic-p-5913.html) (Good | Older | Released 2024 )
- [Rak Wizmesh Tag](https://store.rakwireless.com/products/wismesh-tag-meshtastic-gps-lora-tracker-ip66) (Better | Newer | Released 2025 )
- [Seeed X1 Tracker](https://wiki.seeedstudio.com/meshtracker_x1_intro/) **(Best | Newest | Released 2026 )**

### Meshtastic App
> You connect your phone to your companion device over Bluetooth. You use the messaging function from the Meshtastic app on your phone.

#### Get The App From...
- [Apple App Store](https://apps.apple.com/gb/app/meshtastic/id1586432531)
- [Google Play Store](https://play.google.com/store/apps/details?id=com.geeksville.mesh)
- [F-Droid App Store](https://f-droid.org/en/packages/com.geeksville.mesh)

---

## SHARED CONFIGURATION
**Recommended Settings, To The Benefit Of All**

> **For the most effective mesh**, and the highest certainty that your messages will be delivered reliably, every node at the event uses the same modem/radio settings**... The intention of this guide is to give everyone a reference for settings/configuration so that we're all on **ONE** shared mesh (all contributing to, and benefiting from it together)... This only works if we're all using the same LoRa modem / Radio settings (e.g., same region, same same preset, same frequency slot etc).

 > **Why these settings specifically?**... At festivals/events, you can expect to see a high density of nodes in a small geographic area, whereby range becomes far less of a concern than network congestion. (~60 nodes is approaching the limit of the default "LongFast" preset, where congestion becomes problematic - at a festival we expect to see far more nodes than this, so we must choose settings that overcome the congestion limitations of the default "LongFast" preset!). 

 > **Note**... As we are all sharing the same airwaves, please kindly configure your nodes responsibly and with consideration... If you configure them incorrectly, you will negatively affect everybody's experience (including your own).

### QUICK TIPS

> Device PIN: 123456 - (The default pin when first connecting to your companion device).

> Each time you hit 'Save' your device will restart. Your app may become (temporarily) greyed out during the restart - this is normal.

> Settings are stored on the companion device, not on your phone, so you can setup multiple devices from one phone (e.g., preconfigure them for your friends before handing them out).

### LORA CONFIG

 > Here's the [official recommendation](https://meshtastic.org/blog/why-your-mesh-should-switch-from-longfast) to switch away from the default "LongFast" preset.

| Setting | Value | Notes |
|---|---|---|
| Country/Region | Europe 868mhz | For UK / Europe |
| Preset | Short-Fast | "Short Range - Fast" handles far more nodes than the default Long-Fast preset before becoming congested - see [Presets Documentation](https://meshtastic.org/docs/overview/radio-settings/#presets) |
| Ignore MQTT | ON | We don't need MQTT |
| OK to MQTT | OFF | We don't need MQTT |
| Follow Preset Coding Rate | ON | "Short Fast" Preset Default = 4/5 |
| Number of Hops | 3 | 3 = default (Truly, 3 is fine here) |
| Frequency Slot | 0 | 0 = default |
| RX Boosted Gain | OFF | Uses more battery when on; not required in a dense network at events |
| Frequency Override | OFF / 0 | leave as default |
| Transmit Power | MAX | This varies from device to device. Use the maximum available |
> If a setting isn't in this list, leave it at its default.

### USER CONFIG

| Setting | Value | Notes |
|---|---|---|
| Long Name | -Set your long name- | Set your name so your friends can differentiate you |
| Short Name | -Set your short name- | Set your name so your friends can differentiate you |
> If a setting isn't in this list, leave it at its default.

### DEVICE CONFIG

| Setting | Value | Notes |
|---|---|---|
| Device Role | CLIENT | (see more below) |
| Rebroadcast Mode | Core Portnums Only | Reduces congestion by only rebroadcasting standard packets: NodeInfo, Text, Position, Telemetry, and Routing |
> If a setting isn't in this list, leave it at its default.

> #### Device Role
> - `CLIENT` - For almost ALL nodes. (Any node that you carry around with you).
> - `CLIENT_BASE` - For nodes on top of your camper van / tent / venue. (You probably don't need these at a festival).
> - `ALL_OTHER_ROLES` - Skip these. (These almost certainly aren't relevant for festivals/events).

> #### Avoid ROUTER/REPEATER Role
> Really! You could be hurting the network by incorrectly choosing the `ROUTER` or `REPEATER` role. 
> See: [Avoid ROUTER/REPEATER mode](https://meshtastic.org/docs/configuration/tips/#avoid-routerand-repeater)
> - If at Shambala Festival (UK) - Router nodes have already been placed, you don't need any additional router nodes here.
> - ONLY for EXCEPTIONALLY well-sited nodes (e.g., Central location, 20+ metres up, on a TALL mast, with GOOD antennas).
> - Too many, or poorly placed ROUTER nodes will cause network issues. Official documentation recommends that you only use ROUTER/REPEATER mode if you understand what what the implications are of this mode.

### CHANNEL CONFIG
Meshtastic can be multi-channel (in the same way you might have multiple WhatsApp groups). I reccomend you configure two channels (One public, and one private)...

#### PUBLIC CHANNEL 
  i.e., message everyone within range
  You should have this channel by default, just tweak the settings...
> This channel should appear as 'Primary Channel' / Channel '0'

| Setting | Value | Notes |
|---|---|---|
| Name | -leave-empty- | Don't set a name here, it *MUST BE EMPTY* for the public channel to work properly |
| Key Size | DEFAULT | |
| Key | `AQ==` (Default) | *MUST BE `AQ==`* for the public channel to work properly |
| Channel Role | Primary | |
| Position Requests | OFF | You *MUST DISABLE* location on the public channel for it to work properly on the private channel |
| Precise Location | OFF | You *MUST DISABLE* location on the public channel for it to work properly on the private channel|
| MQTT Uplink | OFF | We don't need MQTT |
| MQTT Downlink | OFF | We don't need MQTT |
> If a setting isn't in this list, leave it at its default.

#### PRIVATE CHANNEL 
  i.e., a private WhatsApp group between only you and your friends
> This channel should appear as 'Secondary Channel' / Channel '1'

| Setting | Value | Notes |
|---|---|---|
| Name | -set-a-name- | Set your group's name |
| Key Size | 256-bit | Enables encryption & channel privacy |
| Key | Auto-Generated | Allow the app to auto-generate your key |
| Channel Role | Secondary | |
| Position Requests | ON (optional) | Lets others on the channel track your location |
| Precise Location | ON (optional) | Shares exact rather than approximate position |
| MQTT Uplink | OFF | We don't need MQTT |
| MQTT Downlink | OFF | We don't need MQTT |
> If a setting isn't in this list, leave it at its default.

#### SHARE YOUR CHANNEL(s)

Each person in your group must add the channel(s) to thier device. The easiest way to do this is: `SETTINGS` > `SHARE QR CODE`


### POSITION CONFIG

> Please be considerate when configuring postions settings. The following settings are recommended to be accurate enough to find your friends without flooding and overwhelming the network with very frequent updates.

| Setting | Value | Notes |
|---|---|---|
| Smart Position | ON | Only sends a position update when the distance/time thresholds below are met, instead of every fixed interval - reduces channel congestion |
| Minimum Interval | 5 Mins | Won't send a position update more often than this, even if moving |
| Minimum Distance | 30 Metres | Won't send a position update unless you've moved at least this far since the last one |
| Device GPS Update Interval | 5 Mins | How often the GPS chip itself takes a fix; keep in line with Minimum Interval so a fix is ready when Smart Position wants to send |
> If a setting isn't in this list, leave it at its default.

---

## Future additions
To-Do / Contributions welcome...

- **Map overlays** - Each year the festival map changes with the new venue layout. We must obtain the new festival map and overlay it to the correct latitude/longitude within the Meshtastic app - doing so enables you to see the location of your friends, relative to the festival layout.
- **Contact festival organisers** - Request placing a ROUTER node on the festival's existing masts. (e.g., atop Main Stage)
- **Where to buy** - Links / Group-buys for companion devices.
