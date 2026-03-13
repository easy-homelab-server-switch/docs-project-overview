|Topic|Publisher|Subscriber(s)|Usage|Supported messages (Payloads)|
| :-: | :-: | :-: | :-: | :-: |
|TOPIC\_CONTROL|Client|Microcontroller|Sending on/off commands|<p>ON</p><p>OFF</p>|
|TOPIC\_SYSTEM|Microcontroller|Server|Sending system commands|SHUTDOWN|
|TOPIC\_HEARTBEAT|Server|Microcontroller|Sending server status|<p>ALIVE</p><p>DEAD</p>|
|TOPIC\_STATE|Microcontroller|Client|Announcing server status|<p>STARTING</p><p>ONLINE</p><p>SHUTTING\_DOWN</p><p>OFFLINE</p>|
|TOPIC\_ESP32\_STATE|Microcontroller|Client|Announcing microcontroller status|<p>ONLINE</p><p>OFFLINE</p>|