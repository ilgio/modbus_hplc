# modbus_hplc
Home Assistant - modbus for HomePLC

Custom component for HomePLC

connection by usb/rs485:
```
modbus:
  name: RS485
  type: serial
  method: rtu
  port: /dev/ttyUSB1
  baudrate: 57600
  stopbits: 1
  bytesize: 8
  timeout: 0.2
  parity: N
  ```
example sensor:
```
sensor:
#Register 204 out 3
  - platform: modbus
    registers:
      - name: light3
        hub: RS485
        register: 204
        out: 3
```        
        
example switch:
```
switch:
  platform: modbus
  registers:
    #Register(400) In(4)
    - name: Stanza 
      hub: RS485
      slave: 1
      register: 400
      command_on: [16]
      command_off: [16]
      #Register(206) Out(1)
      state_on: [206,1,1]
      state_off: [206,1,0]
 ```
