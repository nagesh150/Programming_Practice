# 🧠 Complete Embedded Coding Interview Guide

## For Firmware/Embedded Engineers (Google, Qualcomm, Samsung)

> **Total Questions: 75** | **Focus: Embedded C & Low Level** | **Visualizations: Included**

---

## 📁 Contents

| File                                                 | Topic                | Questions | Description                                         |
| ---------------------------------------------------- | -------------------- | --------- | --------------------------------------------------- |
| [01_c_fundamentals.md](./01_c_fundamentals.md)       | **C Fundamentals**   | 1-15      | `volatile`, `static`, Pointers, Endianness, Structs |
| [02_bits_registers.md](./02_bits_registers.md)       | **Bit Manipulation** | 16-30     | Setting/Clearing bits, Masking, Shifts              |
| [03_memory_management.md](./03_memory_management.md) | **Memory**           | 31-45     | Stack vs Heap, Sections (.bss, .text), Alignment    |
| [04_rtos_concurrency.md](./04_rtos_concurrency.md)   | **RTOS & OS**        | 46-60     | ISRs, Mutex vs Semaphore, Context Switching         |
| [05_systems_protocols.md](./05_systems_protocols.md) | **Protocols**        | 61-75     | I2C, SPI, UART, Bootloaders, Hardware               |

---

## 🎯 The "Big Five" Questions (Must Know)

If you only have 1 hour, ensure you can explain these perfectly:

1.  **`volatile` keyword**: Why is it needed? (Draw the caching diagram).
2.  **Implications of `static`**: Function scope vs File scope.
3.  **Bit Manipulation**: How to Set, Clear, Toggle, Check a bit.
4.  **Interrupts (ISR)**: What IS allowed? What is NOT allowed?
5.  **Mutex vs Semaphore**: The difference in ownership and usage.

---

## 🏢 Company Specific Suggestions

### **Google (Pixel / Nest / Hardware Teams)**

- Focus deeply on **Concurrency** (Deadlocks, Race Conditions).
- **Memory Layout**: Knowing exactly where variables live.
- **System Design**: "Design an elevator controller" (State Machines).

### **Qualcomm (Modem / BSP)**

- **Bit Manipulation**: Expect hard questions here.
- **OS Concepts**: Priority Inversion, Cache coherency, DMA.
- **Hardware**: Register level debugging.

### **Samsung / Apple / Tesla**

- **Low Level Driver**: "Write a driver for this datasheet".
- **Protocol Details**: I2C vs SPI timing diagrams.
- **Safety**: Watchdogs, Stack Overflow protection.

---

## 🛠️ How to Practice

1.  **Don't just read**: Write the code on paper. Pointer syntax is tricky.
2.  **Draw diagrams**: Use the diagrams in these files as inspiration. If you can draw the stack frame, you understand it.
3.  **Debug mentally**: Look at C code and trace where every byte goes.

**Good Luck!** 🚀
