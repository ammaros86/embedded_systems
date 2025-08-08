UART Communication with DMA (STM32)
This project demonstrates how to use DMA (Direct Memory Access) with UART communication on an STM32 microcontroller. 
The goal is to transfer data efficiently between the MCU and a host without burdening the CPU.

What Does This Program Do?
The program uses USART3 to receive exactly 10 bytes of data via DMA. Once the data is received, it is immediately sent back using DMA again. 
This process runs automatically in a loop, without requiring any CPU intervention between receive/send cycles.

In short:

1. Receives 10 bytes via UART using DMA

2. Copies the received data to a transmit buffer

3. Sends the same 10 bytes back via UART using DMA

4. Repeats continuously

Advantages of Using DMA
DMA stands for Direct Memory Access and allows peripherals (like UART) to read/write directly to RAM without CPU involvement. This brings several benefits:

- Asynchronous data transfer (non-blocking)

- Faster and more efficient than polling or interrupts alone

- Frees up CPU time for other tasks

- Lower power consumption (CPU can sleep or handle more important tasks)

=> Important: Limited to 10 Bytes. In this specific example, the DMA is configured to receive exactly 10 bytes. This is crucial to understand:

If you send more than 10 bytes, the following happens:

- Only the first 10 bytes are received correctly

- The remaining bytes are lost, because the DMA buffer is already full

- No overflow handling is implemented in this simple setup

=> Possible Solutions: Use UART Idle Line Detection to handle variable-length messages
