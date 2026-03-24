<a id="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/easy-homelab-server-switch/docs-project-overview">
    <img src="https://github.com/easy-homelab-server-switch.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">Easy Homelab Server Switch</h3>
<h4 align="center">» Project overview «</h4>
  <p align="center">
    <a href="https://github.com/easy-homelab-server-switch/docs-project-overview/blob/main/README.md"><strong>Explore the docs »</strong></a>
    <br />
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#useful-shortcuts">Useful shortcuts</a>
      <ul>
        <li><a href="#project-overview-useful-shortcuts">Project overview</a></li>
        <li><a href="#cloudflare-useful-shortcuts">Cloudflare</a></li>
        <li><a href="#server-useful-shortcuts">Server</a></li>
        <li><a href="#microcontroller-useful-shortcuts">Microcontroller (ESP32)</a></li>
        <li><a href="#client-useful-shortcuts">Client</a></li>
      </ul>
    </li>
    <li>
      <a href="#about-the-project">About the project</a>
    </li>
    <li>
      <a href="#guide">Guide</a>
    </li>
    <li>
      <a href="#deployment-roadmap">Deployment roadmap</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#key-features">Key features</a></li>
        <li><a href="#requirements">Requirements</a></li>
        <li><a href="#roles">Roles</a></li>
        <li><a href="#my-configuration">My configuration</a></li>
      </ul>
    </li>
    <li>
      <a href="#mqtt-section">MQTT</a>
      <ul>
        <li><a href="#sequence-diagrams">Sequence diagrams</a></li>
        <li><a href="#state-machine-diagrams">State machine diagrams</a></li>
        <li><a href="#communication-architecture">Communication architecture</a></li>
        <li><a href="#messages-dictionary">Messages (payload) dictionary</a></li>
      </ul>
    </li>
  </ol>
</details>

<!-- USEFUL SHORTCUTES -->
## Useful shortcuts
|Module|Repository|README|License|
| :- | :- | :- | :- |
|<a id="project-overview-useful-shortcuts"></a>Project overview|[![project-overview][project-overview-shield]][project-overview-url]|[![project-overview][readme-shield]][project-overview-readme-url]|[![project-overview][license-shield]][project-overview-license-url]|
|<a id="cloudflare-useful-shortcuts"></a>Cloudflare|[![cloudflare][cloudflare-shield]][cloudflare-url]|[![cloudflare][readme-shield]][cloudflare-readme-url]|[![cloudflare][license-shield]][cloudflare-license-url]|
|<a id="server-useful-shortcuts"></a>Server|[![server][server-shield]][server-url]|[![server][readme-shield]][server-readme-url]|[![server][license-shield]][server-license-url]|
|<a id="microcontroller-useful-shortcuts"></a>Microcontroller (ESP32)|[![microcontroller-esp32][microcontroller-shield]][microcontroller-url]|[![microcontroller-esp32][readme-shield]][microcontroller-readme-url]|[![microcontroller-esp32][license-shield]][microcontroller-license-url]|
|<a id="client-useful-shortcuts"></a>Client|[![client][client-shield]][client-url]|[![client][readme-shield]][client-readme-url]|[![client][license-shield]][client-license-url]|

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- ABOUT THE PROJECT -->
# About the project
You can get information about the project on the [official website][about-the-project-url].
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- GUIDE -->
# Guide
If you want to get the system up and running as quickly as possible, consider [following the guide][guide-url].

Alternatively, you can follow the free [deployment roadmap](#deployment-roadmap).

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- DEPLOYMENT ROADMAP -->
# Deployment roadmap (TL;DR)
<a id="deployment-roadmap"></a>
This roadmap provides the essential steps to get EHSS running.

## MQTT Broker
- Use <a href="#my-configuration">MQTT broker</a> of your choice or self-host **Mosquitto**.
- Create three sets of credentials (with Pub/Sub permissions) for: `Server`, `ESP32`, and `Client`.
- Note your Broker URL and Port.

## Cloudflare Worker
#### Option A (With GitHub Pages):
- Create a static "Offline" page repo on GitHub.
- Create a new DNS record (CNAME) in Cloudflare for `username.github.io`
- Create new DNS records (A) on **domain registrar page** following the [GitHub docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain).
- Adjust the configuration file (`wrangler.toml`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/cloudflare/blob/main/README.md#configuration).
- Deploy the worker via Wrangler.
#### Option B (Without GitHub Pages):
- Adjust the configuration file (`wrangler.toml`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/cloudflare/blob/main/README.md#configuration).
- Adjust the `build_offline_page()` function in the `index.js` file to customize the page.
- Deploy the worker via Wrangler.

## Linux Server
- Adjust the configuration file (`config.py`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/server/blob/main/README.md#configuration).
- Deploy via Docker: `sudo docker-compose up -d --build --force-recreate`.

## ESP32
- Use Arduino IDE with ESP32 board support.
- Install the [required libraries](#requirements-arduino-ide).
- Adjust the configuration file (`config.cpp`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/esp32/blob/main/README.md#configuration).
- Upload the firmware to the microcontroler.

## Client App
#### Windows
- Make sure you have <a href="#software">required software</a> installed on the PC.
- Adjust the configuration file (`config.py`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/client/blob/main/README.md#configuration).
#### Android (Optional)
- Make sure you have <a href="#software">required software</a> installed on the VM.
- Adjust the configuration file (`config.py`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/client/blob/main/README.md#configuration).
- Initialize Buildozer.
- Adjust the Buildozer configuration file (`buildozer.spec`) by modifying the [following fields](https://github.com/easy-homelab-server-switch/client/blob/main/README.md#buildozer-configuration).
- Build the Android APK `buildozer -v android debug`.


<!-- GETTING STARTED -->
# Getting started

## Key features
- Remote shutdown of the server
- Remote wake-up of the server
- Real-time status monitoring (via TCP port checks and heartbeats)
- TLS support
- Cross-platform client (Windows, Android)
- Works behind CGNAT (no public IP required)
<p align="right">(<a href="#readme-top">back to top</a>)</p>


## Requirements
Before starting, make sure you have access to the following components and tools:

#### Accounts
- MQTT broker
- Cloudflare account
- GitHub account

#### Hardware
- Linux server with static IP
- Linux VM
- ESP32 microcontroller
- Client device
  - PC with Windows
  - **(optional)** Android phone

#### Software
Depending on which components you deploy, you may need the following tools:

|Device|Tool|
| :-- | :-- |
|Server|Docker|
||Docker Compose|
|PC|Python 3.10+|
||git|
||pip|
||Arduino IDE|
|VM|ADB|
||npm|
||openjdk 17|
||buildozer|

#### Arduino IDE
<a id="requirements-arduino-ide"></a>
|Library|Author|
| :- | :- |
|ArduinoJson|Benoit Blanchon|
|LibSSH-ESP32|Ewan Parker|
|PubSubClient|Nick O'Leary|
|WakeOnLan|a7md0|
<p align="right">(<a href="#readme-top">back to top</a>)</p>


## Roles
#### MQTT Broker
<a id="roles-mqtt-broker"></a>
- Receives MQTT commands (all topics)
- Receives MQTT messages (all topics)
- Routes MQTT commands (all topics)
- Routes MQTT messages (all topics)

#### Cloudflare Worker
<a id="roles-cloudflare-worker"></a>
- Routes traffic when the server is down  
  (no redirects — the user stays on the same URL)
- Displays a static **"Server is offline"** page

#### Linux Server
<a id="roles-linux-server"></a>
- Receives MQTT commands `(TOPIC_SYSTEM)`
- Sends MQTT messages `(TOPIC_HEARTBEAT)`
- Executes server shutdown

#### ESP32 Controller
<a id="roles-esp32-controller"></a>
- Receives MQTT messages `(TOPIC_CONTROL`, `TOPIC_HEARTBEAT)`
- Sends MQTT commands `(TOPIC_SYSTEM)`
- Sends MQTT messages `(TOPIC_STATE`, `TOPIC_ESP32_STATE)`
- Sends WOL magic packets to start the server
- Monitors server state via TCP port checks
- Switches the Cloudflare Worker mode

#### Client Application
<a id="roles-client-application"></a>
- Receives MQTT messages `(TOPIC_STATE`, `TOPIC_ESP32_STATE)`
- Sends MQTT messages `(TOPIC_CONTROL)`
- Opens an SSH window on Windows (LAN)
<p align="right">(<a href="#readme-top">back to top</a>)</p>


## My configuration
#### MQTT
- Cloud broker: [HiveMQ Cloud](https://www.hivemq.com/) `(Free “Serverless” option)`
- Separate users for server, ESP32, and client

#### Cloudflare
- Worker name: `offline-mode`

#### Linux Server
- OS: Ubuntu Server 24.04.3 LTS  
- Kernel: GNU/Linux 6.8.0-101-generic x86_64

#### ESP32 Controller
- Model: [ESP32-C3-MINI-1](https://www.amazon.pl/dp/B0BVQN6SGS)

#### Client

##### PC
- OS: Windows 10 21H2
- [Python: 3.13.7](https://www.python.org/downloads/release/python-3137/)

##### Phone
- OS: Android 16

#### VM (for building Android client and deploying Cloudflare Worker)
- OS: Ubuntu Desktop 24.04.4 LTS
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- MQTT -->
<a id="mqtt-section"></a>
# MQTT

## Sequence diagrams
#### Turning on the server
![Server turning on](/img/mqtt-sequence-diagrams/server-turn-on.png)

#### Turning off the server
![Server turning off](/img/mqtt-sequence-diagrams/server-turn-off.png)

#### Turning on the ESP32
![ESP32 turning on](/img/mqtt-sequence-diagrams/esp32-turn-on.png)

#### Turning on the ESP32
![ESP32 turning off](/img/mqtt-sequence-diagrams/esp32-turn-off.png)
<p align="right">(<a href="#readme-top">back to top</a>)</p>


## State machine diagrams
#### TOPIC_STATE
![Topic state](/img/state-machine-diagrams/topic-state.png)

#### TOPIC_ESP32_STATE
![Topic esp32 state](/img/state-machine-diagrams/topic-esp32-state.png)

#### TOPIC_CONTROL
![Topic control](/img/state-machine-diagrams/topic-control.png)

#### TOPIC_SYSTEM
![Topic system](/img/state-machine-diagrams/topic-system.png)

#### TOPIC_HEARTBEAT
![Topic heartbeat](/img/state-machine-diagrams/topic-heartbeat.png)
<p align="right">(<a href="#readme-top">back to top</a>)</p>


## Communication architecture
|Topic|Publisher|Subscriber(s)|Usage|Supported messages (Payloads)|
| :-: | :-: | :-: | :-: | :-: |
|TOPIC\_CONTROL|Client|Microcontroller|Sending on/off commands|<p>ON</p><p>OFF</p>|
|TOPIC\_SYSTEM|Microcontroller|Server|Sending system commands|SHUTDOWN|
|TOPIC\_HEARTBEAT|Server|Microcontroller|Sending server state|<p>ALIVE</p><p>DEAD</p>|
|TOPIC\_STATE|Microcontroller|Client|Announcing server state|<p>STARTING</p><p>ONLINE</p><p>SHUTTING\_DOWN</p><p>OFFLINE</p>|
|TOPIC\_ESP32\_STATE|Microcontroller|Client|Announcing microcontroller state|<p>ONLINE</p><p>OFFLINE</p>|
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="messages-dictionary"></a>
## Messages (payload) dictionary
|Topic|Message (Payload)|Meaning|Retained?|
| :-: | :-: | :-: | :-: |
|TOPIC\_CONTROL|ON|Server start request|No|
||OFF|Server shutdown request|No|
|TOPIC\_SYSTEM|SHUTDOWN|Server shutdown command|No|
|TOPIC\_HEARTBEAT|ALIVE|Server is active|Yes|
||DEAD|Server is not active|Yes|
|TOPIC\_STATE|STARTING|Server is starting|Yes|
||ONLINE|Server is responding|Yes|
||SHUTTING\_DOWN|Server is shutting down|Yes|
||OFFLINE|Server is not responding|Yes|
|TOPIC\_ESP32\_STATE|ONLINE|ESP32 is active|Yes|
||OFFLINE|ESP32 is not active|Yes|
<p align="right">(<a href="#readme-top">back to top</a>)</p>


[microcontroller-shield]: https://img.shields.io/badge/Microcontroller-8A2BE2
[cloudflare-shield]: https://img.shields.io/badge/Cloudflare-8A2BE2
[client-shield]: https://img.shields.io/badge/Client-8A2BE2
[server-shield]: https://img.shields.io/badge/Server-8A2BE2
[project-overview-shield]: https://img.shields.io/badge/Project%20overview-8A2BE2
[readme-shield]: https://img.shields.io/badge/README-8A2BE2
[license-shield]: https://img.shields.io/badge/LICENSE-8A2BE2

[microcontroller-url]: https://github.com/easy-homelab-server-switch/esp32
[cloudflare-url]: https://github.com/easy-homelab-server-switch/cloudflare
[client-url]: https://github.com/easy-homelab-server-switch/client
[server-url]: https://github.com/easy-homelab-server-switch/server
[project-overview-url]: https://github.com/easy-homelab-server-switch/docs-project-overview

[microcontroller-readme-url]: https://github.com/easy-homelab-server-switch/esp32/blob/main/README.md
[cloudflare-readme-url]: https://github.com/easy-homelab-server-switch/cloudflare/blob/main/README.md
[client-readme-url]: https://github.com/easy-homelab-server-switch/client/blob/main/README.md
[server-readme-url]: https://github.com/easy-homelab-server-switch/server/blob/main/README.md
[project-overview-readme-url]: https://github.com/easy-homelab-server-switch/docs-project-overview/blob/main/README.md

[microcontroller-license-url]: https://github.com/easy-homelab-server-switch/esp32/blob/main/LICENSE
[cloudflare-license-url]: https://github.com/easy-homelab-server-switch/cloudflare/blob/main/LICENSE
[client-license-url]: https://github.com/easy-homelab-server-switch/client/blob/main/LICENSE
[server-license-url]: https://github.com/easy-homelab-server-switch/server/blob/main/LICENSE
[project-overview-license-url]: https://github.com/easy-homelab-server-switch/docs-project-overview/blob/main/LICENSE

[about-the-project-url]: https://3m-code.github.io/easy-homelab-server-switch-page/
[guide-url]: https://3m-code.github.io/easy-homelab-server-switch-page/#guide
