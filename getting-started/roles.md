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
- Receives MQTT commands `(TOPIC_SYSTEM)`
- Sends MQTT messages `(TOPIC_HEARTBEAT)`
- Executes shutdown

### ESP32 Controller
- Receives MQTT messages `(TOPIC_CONTROL`, `TOPIC_HEARTBEAT)`
- Sends MQTT commands `(TOPIC_SYSTEM)`
- Sends MQTT messages `(TOPIC_STATE`, `TOPIC_ESP32_STATE)`
- Sends WOL magic packets to start the server
- Monitors server state via TCP port checks
- Switches Cloudflare Worker mode

### Client Application
- Receives MQTT messages `(TOPIC_STATE`, `TOPIC_ESP32_STATE)`
- Sends MQTT messages `(TOPIC_CONTROL)`
- Opens an SSH window on Windows (LAN)