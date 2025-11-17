# smarthome-shutter-rfbridge


Steps to create a shutter entity

- enable dumping of raw codes
```
  dump:
    - raw
```
- press each button on your remote for the given shutter
    - the codes will be repeated at least 5 times
    - write down the codes
    - it will look something like this: `-1480, 723, -363, 715, -363, 714, -364, 714, -363, 715, -362, 716, -363, 442, -711, 765, -710, 722, -365, 360, -712, 721, -365, 361, -711, 367, -712, 542, -710, 723, -361, 363, -711, 370, -710, 720, -365, 361, -711, 722, -363, 715, -364, 361, -711, 722, -363, 716, -364, 361, -712, 368, -711, 369, -711, 368, -711, 368, -711, 722, -361, 363, -712, 721, -365, 361, -711, 368, -710, 368, -710, 720, -365, 361, -711, 368, -710, 369, -710, 722`

- create a time based shutter entity
```
cover:
  - platform: time_based
    name: "Living Room Shutter"
    id: living_room_left_cover
    
    open_action:
      - remote_transmitter.transmit_raw:
          code: [-100, 7000, <open action code>]
          repeat: 
            times: 6
            wait_time: 0s
    
    close_action:
      - remote_transmitter.transmit_raw:
          code: [-100, 7000, <close action code>]
          repeat: 
            times: 6
            wait_time: 0s
    
    stop_action:
      - remote_transmitter.transmit_raw:
          code: [-100, 7000, <stop action code>]
          repeat: 
            times: 6
            wait_time: 0s
    
    open_duration: 17s
    close_duration: 17s
    has_built_in_endstop: true
    manual_control: false
    assumed_state: true
```
- disable dumping of raw codes