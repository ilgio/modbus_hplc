# Home Assistant - modbus for HomePLC

Now very simple to use the HomePLC relays with the ladder diagram could be all done with an input variable %MX400.0 and in output the physical value of the relay in HomePLC.
Insert in the register, the input variable of the stepper (%MX400.1)
in state: insert the physical value of the relay (%QX0.0)

Example of ladder diagram

<img width="478" alt="example_ladder_image" src="https://github.com/user-attachments/assets/24566087-cabb-4036-b5c6-ba9f87814615" />

example_ladder_hplc.fbd


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

     - name: Scala
       hub: RS485
       slave: 1
       register: "%MX400.0" #Variabile in input del passo-passo
       state: "%QX0.0" #Uscita fisica del rele

     - name: Sala Neon
       hub: RS485
       slave: 1
       register: "%MX400.1"
       state: "%QX3.1"

     - name: Sala Led
       hub: RS485
       slave: 1
       register: "%MX400.2"
       state: "%QX3.3"
 ```
