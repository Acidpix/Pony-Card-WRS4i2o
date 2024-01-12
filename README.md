<img src="./readme/ponycard2.png" alt="Logo" width="400">
<img src="./readme/wrs4i2o.png" alt="Logo" width="400">

# Pony-Card-WRS4i2o

Pony-Card-WRS4i2o is a Wiegand/RS485 capable card for access controle powered by PoE

# Main feature 
  - Powered by PoE or 12V/2A input
  - Power sercurity device like badge reader in 12V/0.5A
  - Comunicate in Wiegand, RS485 or digital input (3V to 24V)
  - Drive 2 output NO/NC relay (230V/5A Max)
  - Can run on WiFi and/or Ethernet (e.g for failover)
  - Ready to Home assistant with EspHOME (Sample config avaliable)
  - Ready to MQTT with Tasmota 

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



