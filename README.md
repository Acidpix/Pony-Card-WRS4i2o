<p align="center" >
<img src="./readme/ponycard2.png" alt="Logo" width="400">
</p>
<p align="center">
<img src="./readme/wrs4i2o.png" alt="Logo" width="200" align="center">
</p>


# Pony-Card-WRS4i2o

Pony-Card-WRS4i2o is a Wiegand/RS485 capable card for access controle powered by PoE

# Main feature 
  - Powered by PoE or 12V/2A input
  - Power sercurity device like badge reader in 12V/0.5A
  - Wiegand or RS485 input selectable by switch
  - In Wiegand mode, 1 digital output (e.g for drive 5V Led or buzzer from badge reader)   
  - 4 digital input (3V to 24V)
  - Drive 2 output NO/NC relay (230V/5A Max)
  - Can run on WiFi and/or Ethernet (e.g for failover)
  - Ready to Home assistant with EspHOME (Sample config avaliable)
  - Ready to MQTT with Tasmota (Base firmware avaliable)
  - -20C° +60C° running continous capability
  - Fit in DIN PLC Box like [this](https://fr.aliexpress.com/i/1005004933689728.html)
  - Dimention : 92.4mm X 87.5  

# Esp32 Pin Mapping 
  - GPIO 0 : Flash write mode Conected to CH340
  - GPIO 1 : UART_TX Conected to CH340
  - GPIO 2 : Free use in pin header
  - GPIO 3 : UART_RX Conected to CH340
  - GPIO 4 : Free use in pin header
  - GPIO 5 : Free use in pin header
  - GPIO 6 - 11 : Reserved by flash memory
  - GPIO 12 : Ethernet PHY Power
  - GPIO 13 : Wiegand D0 or RS485 RX
  - GPIO 14 : Wiegand D1 or RS485 TX
  - GPIO 15 : RS485 DIR or digital out in Wiegand mode (e.g for drive status LED on badge reader)
  - GPIO 16 : Free use in pin header
  - GPIO 17 : EMAC Clock out 180
  - GPIO 18 : MDIO(RMII)
  - GPIO 19 : EMAC TXD0(RMII)
  - GPIO 21 : EMAC TX Enable
  - GPIO 22 : EMAC TXD1(RMII)
  - GPIO 23 : MDC(RMII)
  - GPIO 25 : EMAC RXD0(RMII)
  - GPIO 26 : EMAC RXD1(RMII)
  - GPIO 27 : EMAC RX CRS DV
  - GPIO 32 : Relay 1
  - GPIO 33 : Relay 2
  - GPIO 34 : Digital Input 1 (3V - 24V)
  - GPIO 35 : Digital Input 2 (3V - 24V)
  - GPIO 36 : Digital Input 3 (3V - 24V)
  - GPIO 39 : Digital Input 4 (3V - 24V)

# Wiegand ESPHome example 

``` esphome:
  name: Pony Card WRS4i2o
  friendly_name: Pony_Card_WRS4i2o

esp32:
  board: esp32dev
  framework:
    type: arduino

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: 

ota:
  password: 

ethernet:
  type: LAN8720
  mdc_pin: GPIO23
  mdio_pin: GPIO18
  clk_mode: GPIO17_OUT
  power_pin: GPIO12


globals:
  - id: autorized_badge
    type: int64_t
    restore_value: no
    initial_value: '5562314525698'

wiegand:
  - id: badgereader
    d0: GPIO13
    d1: GPIO14
    on_raw: 
      - if:
          condition:
            labda : 'return value == id(autorized_badge);
          then:
            - switch.toggle: r1
          else:
            - switch.toggle: r2
            - delay : 1s
            - switch.toggle: r2

binary_sensor:
  - platform: gpio
    pin: 
      number: 34
      inverted: true
    name: "input1"
  - platform: gpio
    pin: 
      number: 35
      inverted: true
    name: "input2"
  - platform: gpio
    pin: 
      number: 36
      inverted: true
    name: "input3"
  - platform: gpio
    pin: 
      number: 39
      inverted: true
    name: "input4"


output:
  - platform: gpio
    pin: 32
    id: 'Relay_1'  
  - platform: gpio
    pin: 33
    id: 'Relay_2'    

switch:
  - platform: output
    name: "Relay 1"
    id: "r1"
    output: 'Relay_1'
  - platform: output
    name: "Relay 2"
    id: "r2"
    output: 'Relay_2'
  - platform: gpio
    name: "LED"
    id: "led"
    pin:
      number: 15
      inverted: true 
``` 


# Misc
R49 was unpopulated resistance, because it's just for very old PoE device, support only type 1 PoE and this type need permanante 10mA current drain. But this produce 0.5w of heat and in certain condition make overhead the board, please populate only if your PoE injector dont work without an be careful of probaly over heating in +50C° environement.
