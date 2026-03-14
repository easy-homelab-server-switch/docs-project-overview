|Topic|Publisher|Subscriber(s)|Usage|Supported messages (Payloads)|
| :-: | :-: | :-: | :-: | :-: |
|TOPIC\_CONTROL|Client|Microcontroller|Sending on/off commands|<p>ON</p><p>OFF</p>|
|TOPIC\_SYSTEM|Microcontroller|Server|Sending system commands|SHUTDOWN|
|TOPIC\_HEARTBEAT|Server|Microcontroller|Sending server state|<p>ALIVE</p><p>DEAD</p>|
|TOPIC\_STATE|Microcontroller|Client|Announcing server state|<p>STARTING</p><p>ONLINE</p><p>SHUTTING\_DOWN</p><p>OFFLINE</p>|
|TOPIC\_ESP32\_STATE|Microcontroller|Client|Announcing microcontroller state|<p>ONLINE</p><p>OFFLINE</p>|