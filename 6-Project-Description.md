# Pole-Climbing Robot

A Bluetooth-controlled robot that climbs and descends vertical poles and pipes. It runs on an Arduino Uno, an L298N motor driver and three geared DC motors, and is operated from a smartphone app name Bluetooth RC Controller so nobody has to push the robot to climb the pole by hand.

## Why This Project?

Climbing utility poles, lamp posts and pipes by hand is risky and slow. This robot is a small prototype of a safer alternative: the operator stays on the ground and sends Up, Down and Stop commands over Bluetooth while the robot does the climbing. It could be adapted for inspection, surveillance or light maintenance work.

## How It Grips the Pole

Three motors with wheels are mounted around the pole at 120-degree intervals, forming a triangular grip. This spreads the clamping pressure evenly on all sides, so the robot stays centered and holds firmly while it moves.

The motors are 150 RPM geared DC motors. The low speed and high torque give enough force to fight gravity and surface friction without the wheels slipping.

## How It Works

1. **Power:** 2 3.7V Li-Ion cells in series supply 7.4V. The supply passes through a 3-pin toggle switch that turns the whole robot on and off.
2. **Control:** The Arduino Uno R3 listens for commands from an HC-05 Bluetooth module, which pairs with a phone app.
3. **Driving:** On receiving a command, the Arduino sets the input pins of the L293D driver, and the driver powers the three motors.

| Command | Character | Action |
|---------|-----------|--------|
| Up | `F` | All three motors spin forward and the robot climbs |
| Down | `B` | Motor polarity reverses and the robot descends |
| Stop | `S` | Motors are switched off and the gear ratio helps hold the robot in place |

## Components

| Component | Qty | Purpose |
|-----------|-----|---------|
| Arduino Uno R3 | 1 | Main controller |
| L293D Motor Driver | 1 | Drives the motors |
| HC-05 Bluetooth Module | 1 | Wireless link to the phone |
| 150 RPM DC Gear Motors | 3 | Grip and climb |
| 3.7V Li-Ion Cells | 2 | 7.4V power source (series) |
| 3-Pin Toggle Switch | 1 | Main power switch |

## Wiring

**Motors (L298N)**

| L298N Pin | Arduino Pin | Connected To |
|-----------|-------------|--------------|
| IN1 | 8 | Motor pair (2 motors in parallel, Output A) |
| IN2 | 9 | Motor pair (Output A) |
| IN3 | 10 | Single motor (Output B) |
| IN4 | 11 | Single motor (Output B) |

**Bluetooth (HC-05)**

| HC-05 Pin | Arduino Pin |
|-----------|-------------|
| TX | 2 |
| RX | 3 |
| Vin | 3.3v |
| GND | GND |

Two of the three motors share Output A in parallel, and the third uses Output B.

## Using the Robot

1. Upload the sketch to the Arduino Uno.
2. Switch the robot on and pair your phone with the HC-05 (default PIN is usually `1234` or `0000`).
3. Open a Bluetooth terminal or Arduino controller app and send `F`, `B` or `S`.

## Limitations and Future Improvements

- Motors currently run at full speed, with no speed control. PWM on the L293D enable pins (ENA/ENB) could add this.
- There is no failsafe yet. A timeout that stops the motors when Bluetooth disconnects would improve safety.
- Limit switches or sensors could be added to stop the robot at the top or bottom of the pole.
- A camera module could be mounted for live inspection footage.

## Images

- Top view <img width="3000" height="4000" alt="Structure" src="https://github.com/user-attachments/assets/4e95b8d6-2b93-4125-a6f0-839e103a67a7"/>

- Circuit diagram <img width="1789" height="2285" alt="circuit diagram" src="https://github.com/user-attachments/assets/83e92e8e-a661-4c3a-a5b3-135b84cf5035"/>

- Top view with wiring connection


## License

Open source. Feel free to use and modify for learning and projects.
