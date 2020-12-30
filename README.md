# Home Assistant MiLight MQTT
Controls your miLights bulbs with Home Assistant and [Sidoh ESP8266 MiLights Hub](https://github.com/sidoh/esp8266_milight_hub) with MQTT.<br/>
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
