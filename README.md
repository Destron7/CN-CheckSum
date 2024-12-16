# CN-CheckSum

Computer Networks CheckSum Error Control Protocol.

# Checksum Verification Project

<hr>

## Introduction

In computer networking and data transmission, **checksum** is a value used for error detection. It is a technique used to ensure data integrity during transmission. A checksum is calculated by summing up the values of a message in blocks (usually in binary), and the result (checksum) is sent along with the message. The receiver performs the same calculation on the received data and compares the result with the checksum received. If both values match, the message is assumed to be error-free. If they don't match, an error is detected.

<hr>
### Use of Checksum

- **Error Detection**: Checksum is used in many protocols, including TCP/IP, to detect errors in data transmission.
- **Data Integrity**: It ensures that the data received is the same as the data sent, with no corruption or errors during transmission.
- **Simple Calculation**: It is often used in systems where high-speed checks are required for large amounts of data, such as in networking hardware or data transfer applications.

<hr>
## Project Flow

This project implements a checksum calculation for messages transmitted and received using binary strings. The code calculates the checksum for the sent message, computes the checksum for the received message, and then compares the two values to detect any transmission errors. The results are stored in a CSV file for easy inspection.

### Steps of the Code

1. **Checksum Calculation for Sent Message**:

   - The `findChecksum` function takes a sent message (in binary form) and a packet size `k`. The message is divided into `k`-bit packets.
   - These packets are summed together, and the binary sum is processed to handle overflow bits.
   - The final checksum is the complement of the sum.

2. **Receiver's Checksum Calculation**:

   - The `checkReceiverChecksum` function works similarly to the sender's checksum but also includes the checksum in the sum of the received message.
   - The checksum is then complemented, and the result is compared with the sender's checksum.

3. **Processing the CSV File**:

   - The program reads a CSV file containing two columns: one for the sent messages and one for the received messages.
   - The code processes each row in the CSV file, calculating and comparing checksums for each pair of messages.

4. **Comparison and Error Detection**:

   - The checksums are compared. If the sum of the sender's checksum and the receiver's checksum is zero (after the complement), it means no error was detected.
   - If the sum is non-zero, an error is detected.
   - The result of the comparison (`0` for no error, `1` for error) is appended to a list.

5. **Updating the CSV**:
   - The final error status is added as a new column, `ContainsError`, to the DataFrame.
   - The updated DataFrame is then saved back to a new CSV file (`messages_updated.csv`), which contains the error status for each message pair.

### Python Code Flow

1. **Import Libraries**:

   - The code uses the `pandas` library to handle the CSV file and store the data in a DataFrame.
   - The `numpy` library is used to handle missing values (`NaN`).

2. **Functions**:

   - `findChecksum`: Calculates the checksum for the sent message.
   - `checkReceiverChecksum`: Calculates and checks the checksum for the received message.

3. **Main Loop**:

   - The code iterates through each row of the DataFrame (`messages`) containing the sent and received messages.
   - For each row, the checksum for the sent message is computed and compared with the checksum for the received message.
   - The result is stored in the `ContainsError` column (1 for error, 0 for no error).

4. **Saving the Data**:
   - After processing all rows, the updated DataFrame is saved as a new CSV file, `messages_updated.csv`.

### Example

Here’s how the program works:

1. **Input CSV (`messages.csv`)**:
   SentMessage,ReceivedMessage
   10010101011000111001010011101100,10010101011000111001010011101100
   10101010101010101010101010101010,10101010101010101010101010101000
   11001100110011001100110011001100,11001100110011001100110011001101

2. **Output CSV (`messages_updated.csv`)**:
   SentMessage,ReceivedMessage,ContainsError
   10010101011000111001010011101100,10010101011000111001010011101100,0
   10101010101010101010101010101010,10101010101010101010101010101000,1
   11001100110011001100110011001100,11001100110011001100110011001101,1

### Conclusion

This project demonstrates how checksums can be used to detect errors in messages. The checksum calculation involves breaking messages into smaller packets, summing them, and performing a bitwise complement. The process is automated using Python and pandas, and the results are stored in CSV format for easy analysis.
