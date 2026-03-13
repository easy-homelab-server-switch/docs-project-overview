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