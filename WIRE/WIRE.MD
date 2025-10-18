## Wiring Schematics

| Connection          | From                        | To                                           | Notes                                             |
|---------------------|-----------------------------|----------------------------------------------|---------------------------------------------------|
| **Power (5V, GND)** | Controller                  | MKS Express + Receiver                       | Common 5V and GND for both                        |
| **CAN Bus**         | Controller (CL, CH)         | MKS Express (CAN-L, CAN-H)                   | For VESC logging and Bluetooth via the VESC Express |
| **UART**            | Controller (TX, RX)         | Receiver (RX, TX, GND)                       | For telemetry / remote uplink                     |
| **PPM**             | Receiver (PPM output)       | Controller (PPM input or signal out to VESC) | For throttle / RC control                         |
