1. Roles:
   1. MQTT broker
      1. Receives MQTT commands
      1. Receives MQTT messages
      1. Passes on MQTT commands
      1. Passes on MQTT messages
   1. Cloudflare Worker
      1. Displays static “Server is offline” page
      1. Routes traffic when server is down (not redirects, user stays on the same page)
   1. Linux server
      1. Receives MQTT commands
      1. Sends MQTT messages (own state – heartbeat)
      1. Executes shutdown
   1. ESP32 controller
      1. Receives MQTT commands
      1. Receives MQTT messages
      1. Sends MQTT commands
      1. Sends MQTT messages (own state, server state after verification)
      1. Sends WOL magic packets to start the server
      1. Monitors server state via TCP port check
      1. Switches Cloudflare worker
   1. Client app
      1. Receives MQTT messages (esp32 state, server state)
      1. Sends MQTT commands (turn on, turn off)
      1. Can open SSH window on Windows