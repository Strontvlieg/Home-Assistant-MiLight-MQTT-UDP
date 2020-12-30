# Home Assistant MiLight with MQTT
Controls your miLights V6 bulbs with Home Assistant and [Sidoh ESP8266 MiLight Hub](https://github.com/sidoh/esp8266_milight_hub) with MQTT.<br/>
<h3>Setup Sidoh ESP8266 MiLight Hub</h3>
<p>
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
When u ready it looks like this:
<img src="https://github.com/Strontvlieg/Home-Assistant-MiLight-MQTT/blob/main/hub.png">
</p>
<h3>Setup Home Assistant</h3>
<h4>configuration.yaml</h4>
<p>
<pre><code class="language-yaml">
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
</code></pre>
</p>
