# UART Communication with DMA (STM32)
This project demonstrates how to use DMA (Direct Memory Access) with UART communication on an STM32 microcontroller. 
The goal is to transfer data efficiently between the MCU and a host without burdening the CPU.

What Does This Program Do?
The program uses USART3 to receive exactly 10 bytes of data via DMA. Once the data is received, it is immediately sent back using DMA again. 
This process runs automatically in a loop, without requiring any CPU intervention between receive/send cycles.

In short:

1. Receives 10 bytes via UART using DMA (1234567890)

2. Copies the received data to a transmit buffer

3. Sends the same 10 bytes back via UART using DMA

4. Repeats continuously

 <img width="619" height="538" alt="image" src="https://github.com/user-attachments/assets/6a0272f7-34f2-47aa-8dbe-4eb9154fc4af" />


## Advantages of Using DMA
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

Projct:
We use UART 3 in this example for communication between the STM32 and the computer. The baud rate is 115200, with a word length of 8 bits and 1 stop bit. The rest of the configuration is set to default, as shown in the screenshot below.

<img width="899" height="710" alt="image" src="https://github.com/user-attachments/assets/bce7f434-e538-4c06-b93c-0ee664425109" />

We enable the USART3_RX DMA (Direct Memory Access) for communication between the peripheral (USART3) and memory, where data is transferred from the peripheral to memory. For the USART3_TX, we configure the DMA to transfer data from memory to the peripheral.

In addition, we set the RX DMA to circular mode. This ensures that the DMA continuously writes incoming data to the buffer without interruption, allowing the program to receive data without missing any. In circular mode, once the DMA buffer is full, it automatically wraps around and starts overwriting the oldest data, ensuring that new data is always written into the buffer.

<img width="900" height="539" alt="image" src="https://github.com/user-attachments/assets/09d5b567-a199-4987-beda-ca9fa0ec45cf" />


