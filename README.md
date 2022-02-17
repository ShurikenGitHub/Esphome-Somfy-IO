# Esphome-Somfy-IO

This code allows you to control a Somfy Smoove Origin 4 IO remote from esphome/homeassistant.
The IO protocol can't be "copied" like the RTS protocol because it's encrypted so an invasive solution is required.

To overcome not being able to copy the commands, I soldered wires to the buttons to mimic a buttonpress.
I guess this sort of "botches" a working remote, but it works really well and is much cheaper €65 than buying a Somfy Connexoon IO of €150. (*We only have 4 shutters*)
The code also adds additional functionality like pausing the shutter at a desired percentage (10% down for example).

It is a good idea to first learn in the devices to the remote, because if you want to do it after the conversion it's a bit of a pain.

# Soldering

I used 28AWG wire. First add more solder to the buttonjoint and don't keep the soldering iron on there for too long because it will melt the pad.

On the frontside I soldered wires to the green circles. The wires are connected to the Esp8266 as follows:
- 1 D5
- 2 D6
- 3 D7
- 4 RX
- Up D0
- My D1
- Down D2

![image](https://user-images.githubusercontent.com/61755262/154518948-17897879-378a-4965-8e64-f8d0d9d4a284.png)

On the backside I soldered a 3.3V pin from the MCU to the plus pad (with the 2 little arms) and the ground from the MCU to the groundpad (the lowest one).
DONT USE 5V, IT WILL PROBABLY DESTROY THE REMOTE IMMEDIATELY.

# Code
The following entities are published to home assistant (though the right colomn is disabled by default).
![image](https://user-images.githubusercontent.com/61755262/154526427-100ec5cb-bd77-4401-a09f-660739c53624.png)

With the custom:slider-entity-row card (available in the HACS store), you can control the percentage from the main dashboard.
Simply add this code under the entity name in the card code editor:
```
  - type: custom:slider-entity-row
    entity: cover.cover_1
    full_row: true
```    
![image](https://user-images.githubusercontent.com/61755262/154527246-d62be0ee-93b4-4e8b-b7e9-ae127aafbcc5.png)

