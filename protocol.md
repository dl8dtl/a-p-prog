# Serial protocol

## Introduction

The serial protocol between `pp3` and the firmware is a simple
request-response protocol.

Each request contains of a command-byte, followed by a second
byte indicating how many further bytes are being transferred
from the host.  If the second byte is zero, no further bytes
are transferred.

## Commands

| byte | args            | remark                         | response        |
| ---- | ----------------| -------------------------------|-----------------|
| 0x01 | none            | enter progmode PIC16 A/B/D     | 0x81            |
| 0x02 | none            | exit progmode                  | 0x82            |
| 0x03 | none            | reset pointer PIC16 A/B        | 0x83            |
| 0x04 | none            | load config PIC16              | 0x84            |
| 0x05 | count           | increment pointer by count     | 0x85            |
| 0x06 | count           | read page, count 16-bit words  | 0x86, data      |
| 0x07 | none            | mass erase PIC16 A/B/D         | 0x87            |
| 0x08 | count, data     | write page, count 16-bit words | 0x88            |
| 0x09 | none            | reset pointer PIC16 D          | 0x89            |
| 0x10 | none            | enter progmode PIC18           | 0x90            |
| 0x11 | count, 3*addr   | read page PIC18, count 16-bit  | 0x91, data      |
|      |                 | words, 24-bit address          |                 |
| 0x12 | count, 3*addr,  | write page PIC18, count 16-bit | 0x92            |
|      | data            | words, 24-bit address          |                 |
| 0x13 | none            | mass erase PIC18A              | 0x93            |
| 0x14 | 4*addr, 2*data  | PIC18A write config            | 0x94            |
| 0x23 | none            | PIC18B mass erase              | 0xa3            |
| 0x30 | 3*addr          | PIC18D mass erase part         | 0xb0            |
| 0x31 | count, 3*addr,  | PIC18D write page              | 0xb1            |
|      | data            |                                |                 |
| 0x32 | 4*addr, 2*data  | PIC18D write config            | 0xb2            |
| 0x40 | none            | PIC16C enter progmode          | 0xc0            |
| 0x41 | count, 3*addr   | PIC16C read page, count 16-bit | 0xc1, data      |
|      |                 | words, 24-bit address          |                 |
| 0x42 | count, 3*addr,  | PIC16C write page, count 16-bit| 0xc2            |
|      | data            | words, 24-bit address          |                 |
| 0x43 | none            | PIC16C mass erase              | 0xc3            |
| 0x44 | 4*addr, 2*data  | PIC16C write config            | 0xc4            |
| 0x45 | 4*addr, 2*data  | PIC18Q write config            | 0xc5            |
| 0x46 | count, 3*addr,  | PIC18Q write page, count 16-bit| 0xc6            |
|      | data            | words, 24-bit address          |                 |
