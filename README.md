# Home-Assistant-MiLight-MQTT

<h4>configuration.yaml</h4>
<p>
light:<br>
  - platform: mqtt<br>
    name: Voorkamer<br>
    schema: json<br>
    command_topic: "milight/commands/0x1000/rgb_cct/1"<br>
    state_topic: "milight/states/0x1000/rgb_cct/1"<br>
    brightness: true<br>
    rgb: true<br>
    color_temp: true<br>
    effect: true<br>
    effect_list:<br>
      - '0'<br>
      - '1'<br>
      - '2'<br>
      - '3'<br>
      - '4'<br>
      - '5'<br>
      - '6'<br>
      - '7'<br>
      - '8'<br>
      - white_mode<br>
      - night_mode<br>
    optimistic: true<br>
    qos: 0<br>
</p>
