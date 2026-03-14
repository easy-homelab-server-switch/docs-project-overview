## Roles

### MQTT Broker
- Receives MQTT commands (all topics)
- Receives MQTT messages (all topics)
- Forwards MQTT commands (all topics)
- Forwards MQTT messages (all topics)

### Cloudflare Worker
- Routes traffic when the server is down  
  (no redirects — the user stays on the same URL)
- Displays static **"Server is offline"** page

### Linux Server
- Receives MQTT commands (TOPIC\_SYSTEM)
- Sends MQTT messages (TOPIC\_HEARTBEAT)
- Executes shutdown

### ESP32 Controller
- Receives MQTT messages (TOPIC\_CONTROL, TOPIC\_HEARTBEAT)
- Sends MQTT commands (TOPIC\_SYSTEM)
- Sends MQTT messages (TOPIC\_STATE, TOPIC\_ESP32\_STATE)
- Sends WOL magic packets to start the server
- Monitors server state via TCP port checks
- Switches Cloudflare Worker mode

### Client Application
- Receives MQTT messages (TOPIC\_STATE, TOPIC\_ESP32\_STATE)
- Sends MQTT messages (TOPIC\_CONTROL)
- Opens an SSH window on Windows (LAN)