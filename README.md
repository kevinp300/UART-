# UART-
The UART (Universal Asynchronous Receiver Transmitter) involves implementing a serial communication interface using Verilog and RTL (Register-Transfer Level) techniques. This project includes a transmitter (uart_tx module) and a receiver (uart_rx module) that communicate using asynchronous serial communication. The project uses a data rate of 9600 bps, a data width of 8 bits, and a standard 1 stop bit format. However, it does not include parity bit generation or checking, and does not have any flow control options implemented.

The Verilog code for the UART project includes two main modules, uart_tx and uart_rx, which represent the transmitter and receiver respectively. The uart_tx module receives parallel data (data signal) and serializes it for transmission as a series of bits (tx signal) with a start bit, followed by the data bits, and then a stop bit. The uart_rx module receives the serial data (rx signal) and deserializes it back into parallel data (data signal) by detecting the start and stop bits.

The baud_rate_generator module is used to generate the clock signal for the UART communication, which determines the data rate. In this example, a baud rate of 9600 bps is used, but this can be modified to a different value depending on the desired data rate for the specific application.

Inputs:

clk: Clock input for both transmitter and receiver modules.
rst_n: Reset input (active low) for both transmitter and receiver modules.
data: 8-bit data input for the transmitter module.
tx_en: Transmission enable input for the transmitter module.
rx: Received serial data input for the receiver module.
rx_en: Reception enable input for the receiver module.
parity: Parity bit input (0 for even, 1 for odd, 2 for no parity) for the receiver module.
stop_bits: Number of stop bits input (0 for 1 stop bit, 1 for 1.5 stop bits, 2 for 2 stop bits) for the receiver module.
Outputs:

tx: Transmitted serial data output from the transmitter module.
txc: Transmission complete output from the transmitter module.
data: Received data output from the receiver module.
rxc: Reception complete output from the receiver module.
Internal Signals:

uart_data: 10-bit data register (including start, data, parity, and stop bits) in the transmitter module.
uart_state: 4-bit state register for FSM (Finite State Machine) in both transmitter and receiver modules.
count: 4-bit counter for data and stop bits in the transmitter module.
parity: 3-bit parity bit in the transmitter module.
stop_bits: 3-bit number of stop bits in the transmitter module.
flow_ctrl: 3-bit flow control option in the transmitter module.
States:

IDLE: 3-bit state representing the idle state in both transmitter and receiver modules.
START: 3-bit state representing the start bit state in the transmitter module.
DATA: 3-bit state representing the data bit state in the transmitter module.
PARITY: 3-bit state representing the parity bit state in the transmitter module.
STOP: 3-bit state representing the stop bit state in the transmitter module.
Functionality:

The transmitter module (uart_tx) takes input data, generates serial data with start, data, parity, and stop bits, and outputs it through the tx signal. It uses a finite state machine (FSM) to control the timing of the transmission.
The receiver module (uart_rx) takes input serial data, extracts the received data by removing the start, parity, and stop bits, and outputs it through the data signal. It also outputs a reception complete signal (rxc) when the entire data is received. The receiver module also takes input control signals for enabling and controlling the reception process.
