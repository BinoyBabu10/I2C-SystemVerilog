# I2C Master Controller – SystemVerilog

A fully functional I2C Master Controller implemented in SystemVerilog, supporting both **read** and **write** operations with ACK/NACK handling and a configurable clock divider.

---

## 📌 Project Overview

This project implements an I2C Master that communicates with I2C Slave devices over the standard two-wire protocol (SDA and SCL). The design is written in synthesizable SystemVerilog and includes a self-contained testbench for functional verification.

**Target Frequency:** 40 MHz system clock → 100 KHz I2C clock (Standard Mode)

---

## ✨ Features

- ✅ I2C Master with Start / Stop condition generation
- ✅ 7-bit slave address support
- ✅ Write and Read operations (controlled via `op` signal)
- ✅ ACK / NACK detection with `ack_err` flag
- ✅ Configurable system and I2C frequency via parameters
- ✅ FSM-based design with 9 states: `idle → start → write_addr → ack_1 → write_data / read_data → ack_2 → master_ack → stop`
- ✅ Tri-state SDA bus handling
- ✅ SystemVerilog interface for clean testbench integration

---

## 🗂️ File Structure

| File | Description |
|------|-------------|
| `design.sv` | I2C Master RTL design + interface definition |
| `testbench.sv` | Functional testbench for write and read operations |

---

## 🔧 Module Interface
```verilog
module i2c_master (
  input        clk,      // System clock (40 MHz)
  input        rst,      // Active-high synchronous reset
  input        newd,     // New data trigger
  input  [6:0] addr,     // 7-bit slave address
  input        op,       // Operation: 0 = Write, 1 = Read
  inout        sda,      // I2C Serial Data Line (tri-state)
  output       scl,      // I2C Serial Clock Line
  input  [7:0] din,      // Data to write to slave
  output [7:0] dout,     // Data received from slave
  output reg   busy,     // High when transaction is in progress
  output reg   ack_err,  // High if slave sends NACK
  output reg   done      // Pulses high when transaction completes
);
```

---

## 🔄 FSM State Diagram
```
IDLE → START → WRITE_ADDR → ACK_1 → WRITE_DATA → ACK_2 → STOP
                                  ↘ READ_DATA → MASTER_ACK → STOP
```

---

## ▶️ How to Simulate

You can simulate this project on [EDA Playground](https://www.edaplayground.com/) or any SystemVerilog-compatible simulator (ModelSim, QuestaSim, Icarus Verilog + sv support).

1. Clone this repository:
```bash
   git clone https://github.com/BinoyBabu10/I2C-SystemVerilog.git
```
2. Open `design.sv` and `testbench.sv` in your simulator.
3. Compile and run the testbench.
4. Observe waveforms for SCL, SDA, `done`, and `ack_err` signals.

---

## 🧠 Concepts Demonstrated

- Serial communication protocol (I2C)
- Finite State Machine (FSM) design in SystemVerilog
- Tri-state bus control
- Clock divider and pulse generation
- ACK/NACK handshaking
- SystemVerilog interfaces and testbench writing

---

## 🛠️ Tools & Technologies

- **Language:** SystemVerilog
- **Simulator:** EDA Playground / ModelSim
- **Protocol:** I2C (Inter-Integrated Circuit)

---

## 👤 Author

**Binoy Babu**  
[GitHub Profile](https://github.com/BinoyBabu10)
