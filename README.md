# Home Assistant MiLight with MQTT
Controls your miLights V6 bulbs with Home Assistant and [Sidoh ESP8266 MiLight Hub](https://github.com/sidoh/esp8266_milight_hub) with MQTT.<br/>

<p>
<h3>Setup the ESP8266 MiLight Hub</h3>
Click on: Settings/MQTT
<table>
<tr>
<td>MQTT server</td>
<td>Server IP</td>
</tr>
<tr>
<td>MQTT topic pattern</td>
<td>milight/commands/:device_id/:device_type/:group_id</td>
</tr>
<tr>
<td>MQTT update topic pattern</td>
<td>mililight/updates/:device_id/:device_type/:group_id</td>
</tr>
<tr>
<td>MQTT state topic pattern</td>
<td>milight/states/:device_id/:device_type/:group_id</td>
</tr>
<tr>
<td>MQTT user name</td>
<td>Username</td>
</tr>
<tr>
<td>MQTT password</td>
<td>Password</td>
</tr>
<tr>
<td>MQTT Client Status Topic</td>
<td>milight/status/:device_id/:device_type/:group_id</td>
</tr>
<tr>
<td>Publish state messages with retain flag</td>
<td>Enabled</td>
</tr>
<tr>
<td>Client Status Messages Mode</td>
<td>Detailed</td>
</tr>
<tr>
<td>HomeAssistant MQTT Discovery Prefix</td>
<td></td>
</tr>
<tr>
<td>MQTT state rate limit</td>
<td>500</td>
</tr>
<tr>
<td>MQTT debounce delay</td>
<td>500</td>
</tr>
</table>
</br>
Click on: Settings/UDP
<table>
<tr>
<td>Device ID</td>
<td>0x1000</td>
</tr>
<tr>
<td>UDP Port</td>
<td>5987</td>
</tr>
<tr>
<td>Protocol Version</td>
<td>6</td>
</tr>
</table>
</br>


When it's ready it looks like this:
<h4>MQTT</h4>
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/mqtt.png">
<h4>UDP</h4>
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/udp.png">
</p>

<p>
Choose between MQTT or UDP and add this configuration to Home Assistant
</P

<p>
<h3>Setup Home Assistant for MQTT</h3>
<h4>configuration.yaml</h4>
<pre><code class="language-yaml">
# Setup the MQTT broker
mqtt:
  broker: 192.168.1.101
  port: 1883
  client_id: home-assistant-1
  keepalive: 60
  discovery: true
</code></pre>

<pre><code class="language-yaml">
# Setup the MiLights
light:
  - platform: mqtt
    name: Voorkamer
    schema: json
    command_topic: "milight/commands/0x1000/rgb_cct/1"
    state_topic: "milight/states/0x1000/rgb_cct/1"
    brightness: true
    rgb: true
    color_temp: true
    effect: true
    effect_list:
      - '0'
      - '1'
      - '2'
      - '3'
      - '4'
      - '5'
      - '6'
      - '7'
      - '8'
      - white_mode
      - night_mode
    optimistic: true
    qos: 0
  - platform: mqtt
    name: Achterkamer
    schema: json
    command_topic: "milight/commands/0x1000/rgb_cct/2"
    state_topic: "milight/states/0x1000/rgb_cct/2"
    brightness: true
    rgb: true
    color_temp: true
    effect: true
    effect_list:
      - '0'
      - '1'
      - '2'
      - '3'
      - '4'
      - '5'
      - '6'
      - '7'
      - '8'
      - white_mode
      - night_mode
    optimistic: true
    qos: 0
</code></pre>


<h3>Setup Home Assistant for UDP</h3>
<h4>configuration.yaml</h4>
<pre><code class="language-yaml">
# Setup the MiLights
light:
  - platform: limitlessled
    bridges:
      - host: 192.168.1.102
        port: 5987
        version: 6
        groups:
          - number: 1
            name: Voorkamer
            type: rgbww
            fade: false
          - number: 2
            name: Achterkamer
            type: rgbww
            fade: false
</code></pre>
</p>
