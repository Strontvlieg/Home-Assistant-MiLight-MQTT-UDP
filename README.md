# Home Assistant MiLight with MQTT or UDP
Controls your miLights V6 bulbs with Home Assistant and [Sidoh ESP8266 MiLight Hub](https://github.com/sidoh/esp8266_milight_hub) with MQTT or UDP.<br/>

<h1>MQTT</h1>
<p>
<h3>Setup the ESP8266 MiLight Hub</h3>
On the ESP8266 MiLight Hub click on: Settings/MQTT
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
<td>
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
On the ESP8266 MiLight Hub click on: Settings/UDP
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
</br>
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/mqtt.png">
</br>
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/udp.png">
</br>
</br>
If you now monitor the MQTT server with MQTT.fx you will see the following information.
</br>
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/fx.png">
</br>
</br>
Look at the MQTT message on you server. They are automatically filled in with the correct information, this message is from: milight/states/:device_id/:device_type/:group_id
</br>
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/mqtt_string.png">
</br>
red = device_id / green = device_type / blue = group


</br>
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
light:
  - name: MiLight 0x1000 Zone 0
    unique_id: milight_0x1000_zone_0
    command_topic: "milight/commands/0x1000/rgb_cct/0"
    state_topic: "milight/states/0x1000/rgb_cct/0"
    
    # Use YAML anchor for common settings for other MiLights.
    <<: &MILIGHTS_RGBCCT_PARAMS
      platform: mqtt
      schema: json
      brightness: true
      color_temp: true
      rgb: true
      effect: true
      effect_list:
        - night_mode
        - white_mode
        - '0'
        - '1'
        - '2'
        - '3'
        - '4'
        - '5'
        - '6'
        - '7'
        - '8'

  - name: MiLight 0x1000 Zone 1
    unique_id: milight_0x1000_zone_1
    command_topic: "milight/commands/0x1000/rgb_cct/1"
    state_topic: "milight/states/0x1000/rgb_cct/1"
    <<: *MILIGHTS_RGBCCT_PARAMS

  - name: MiLight 0x1000 Zone 2
    unique_id: milight_0x1000_zone_2
    command_topic: "milight/commands/0x1000/rgb_cct/2"
    state_topic: "milight/states/0x1000/rgb_cct/2"
    <<: *MILIGHTS_RGBCCT_PARAMS

  - name: MiLight 0x1000 Zone 3
    unique_id: milight_0x1000_zone_3
    command_topic: "milight/commands/0x1000/rgb_cct/3"
    state_topic: "milight/states/0x1000/rgb_cct/3"
    <<: *MILIGHTS_RGBCCT_PARAMS

  - name: MiLight 0x1000 Zone 4
    unique_id: milight_0x1000_zone_4
    command_topic: "milight/commands/0x1000/rgb_cct/4"
    state_topic: "milight/states/0x1000/rgb_cct/4"
    <<: *MILIGHTS_RGBCCT_PARAMS
</code></pre>
</p>


</br>
</br>
<h1>UDP</h1>
<p>
<h3>Setup the ESP8266 MiLight Hub</h3>
On the ESP8266 MiLight Hub click on: Settings/UDP
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
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/udp.png">
</br>


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
          - number: 0
            name: MiLight 0x1000 0
            type: rgbww
            fade: false
          - number: 1
            name: MiLight 0x1000 1
            type: rgbww
            fade: false
          - number: 2
            name: MiLight 0x1000 2
            type: rgbww
            fade: false
          - number: 3
            name: MiLight 0x1000 3
            type: rgbww
            fade: false
          - number: 4
            name: MiLight 0x1000 4
            type: rgbww
            fade: false
</code></pre>
</p>
