# Motor Driver Circuit Explanation
![motor sch](https://github.com/user-attachments/assets/e1950ef7-11e8-436f-ae37-db34f568c9ab)
![motor pcb](https://github.com/user-attachments/assets/26528681-5ad2-4609-87dd-f703b40dabb8)

This circuit utilizes the L293D to control the direction of two DC motors based on digital input signals. It also includes a 5V regulator for powering the control logic and a power indicator LED.

## Components

* **U1: L293D - Quadruple Half-H Driver:** An integrated circuit containing four half-H bridge drivers, enabling bidirectional control of DC motors.
    * **1A, 2A, 3A, 4A (Input Pins):** Control the output states of the respective half-H bridges.
    * **1Y, 2Y, 3Y, 4Y (Output Pins):** Connect to the terminals of the motors.
    * **EN1,2 (Enable Pins 1 & 2):** Enable/disable the first two drivers (controlling outputs 1Y and 2Y).
    * **EN3,4 (Enable Pins 3 & 4):** Enable/disable the last two drivers (controlling outputs 3Y and 4Y).
    * **VCC1 (Pin 16):** Logic supply voltage (5V).
    * **VCC2 (Pin 8):** Motor supply voltage.
    * **GND (Pins 4, 5, 12, 13):** Ground connections.

* **U3: L7805 - 5V Voltage Regulator:** A linear regulator that provides a stable 5V output for the logic circuitry.
    * **IN (Pin 1):** Input for the higher voltage supply.
    * **GND (Pin 2):** Ground connection.
    * **OUT (Pin 3):** Regulated 5V output (**PWR\_FLAG**).

* **J1: Conn\_01x04\_Pin - Control Input Connector:** A 4-pin connector for applying digital control signals to the L293D.

* **J2: Screw\_Terminal\_01x02 - Motor Power Input:** A 2-pin screw terminal for connecting the higher voltage power supply for the motors and the input of the L7805.

* **J3: Screw\_Terminal\_01x02 - Motor Output 1:** A 2-pin screw terminal for connecting the first motor.

* **J4: Screw\_Terminal\_01x02 - Motor Output 2:** A 2-pin screw terminal for connecting the second motor.

* **D1: LED - Power Indicator:** An LED that illuminates when the 5V power supply is active.

* **R1: 1kΩ Resistor:** A current-limiting resistor for the power indicator LED.

* **PWR\_FLAG:** Net label for the regulated 5V power supply rail.

* **GND:** Net label for the common ground connection.

## Working Principle

1.  **Logic Power:** A higher DC voltage is supplied to **J2**. The **L7805 (U3)** regulates this voltage to 5V (**PWR\_FLAG**), powering the control logic of the **L293D (VCC1)**. The **LED (D1)** indicates the presence of this 5V.

2.  **Motor Power:** The higher DC voltage from **J2** also powers the motor driving stage of the **L293D (VCC2)**.

3.  **Control Inputs:** Digital signals applied to **J1** are fed into the input pins (1A, 2A, 3A, 4A) and enable pins (EN1,2, EN3,4) of the **L293D**.

4.  **Enabling Motors:** To drive a motor connected to **J3** or **J4**, the corresponding enable pin(s) on the **L293D** must be high.

5.  **Direction Control:** The logic levels on the input pins (e.g., 1A and 2A for the motor at **J3**) determine the direction of current flow through the motor, thus controlling its rotation direction. The **L293D** internally switches the power to the motor based on these inputs.

6.  **Motor Output:** The **L293D** outputs the controlled power to the motors connected at **J3** and **J4**, allowing for bidirectional control of two independent DC motors.
