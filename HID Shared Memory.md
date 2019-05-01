HID shared memory is a 0x40000 byte read-only segment of memory shared
between applications for input. The segment contains structures for most
if not all input methods available to applications.

# Memory Map

| Offset  | Size in bytes | Description                                                                |
| ------- | ------------- | -------------------------------------------------------------------------- |
| 0x0     | 0x400         | Unknown, Header?                                                           |
| 0x400   | 0x3000        | Capacitive Touchscreen                                                     |
| 0x3400  | 0x400         | Mouse                                                                      |
| 0x3800  | 0x400         | Keyboard                                                                   |
| 0x3C00  | 0x400         | Unknown, header and 17 entries                                             |
| 0x4000  | 0x400         | Unknown, header and 17 entries                                             |
| 0x4400  | 0x400         | Unknown, header and 17 entries                                             |
| 0x4800  | 0x400         | Unknown, header and 17 entries                                             |
| 0x4C00  | 0x200         | Unknown, header which says it has 17 entries, but the max entry index is 0 |
| 0x4E00  | 0x200         | Unknown, header which says it has 17 entries, but the max entry index is 0 |
| 0x5000  | 0x200         | Unknown, header which says it has 17 entries, but the max entry index is 0 |
| 0x5200  | 0x80\*0x10    | Unknown, 16 structures with a header and 2 entries each                    |
| 0x5A00  | 0x4000        | Controller Serials?                                                        |
| 0x9A00  | 0x32000       | Controllers                                                                |
| 0x3BA00 | 0x4600        | Unknown                                                                    |
| 0x3C200 | ?             | \[5.0.0+\] SevenSixAxisSensor                                              |
|         |               |                                                                            |

## Capacitive Touchscreen

| Offset | Size in bytes | Description   |
| ------ | ------------- | ------------- |
| 0x0    | 0x28          | Touch Header  |
| 0x28   | 0x298 \* 17   | Touch Entries |
|        |               |               |

### Touch Header

| Offset | Size in bytes | Description                    |
| ------ | ------------- | ------------------------------ |
| 0x0    | 0x8           | Timestamp in ticks?            |
| 0x8    | 0x8           | Number of Entries, always 17   |
| 0x10   | 0x8           | Latest Entry Index             |
| 0x18   | 0x8           | Maximum Entry Index, always 16 |
| 0x20   | 0x8           | Timestamp in samples           |
|        |               |                                |

### Touch Entry

| Offset | Size in bytes | Description        |
| ------ | ------------- | ------------------ |
| 0x0    | 0x10          | Touch Entry Header |
| 0x10   | 0x28 \* 16    | Touch Data         |
|        |               |                    |

#### Touch Structure Header

| Offset | Size in bytes | Description          |
| ------ | ------------- | -------------------- |
| 0x0    | 0x8           | Timestamp in samples |
| 0x8    | 0x8           | Number of Touches    |
|        |               |                      |

#### Touch Data Entry

| Offset | Size in bytes | Description          |
| ------ | ------------- | -------------------- |
| 0x0    | 0x8           | Timestamp in samples |
| 0x8    | 0x4           | Padding              |
| 0xC    | 0x4           | Touch Index          |
| 0x10   | 0x4           | Touch X              |
| 0x14   | 0x4           | Touch Y              |
| 0x18   | 0x4           | Touch Diameter X     |
| 0x1C   | 0x4           | Touch Diameter Y     |
| 0x20   | 0x4           | Angle                |
| 0x24   | 0x4           | Padding              |
|        |               |                      |

## Mouse

| Offset | Size in bytes | Description   |
| ------ | ------------- | ------------- |
| 0x0    | 0x20          | Mouse Header  |
| 0x20   | 0x30 \* 17    | Mouse Entries |
|        |               |               |

### Mouse Header

| Offset | Size in bytes | Description                    |
| ------ | ------------- | ------------------------------ |
| 0x0    | 0x8           | Timestamp in ticks?            |
| 0x8    | 0x8           | Number of Entries, always 17   |
| 0x10   | 0x8           | Latest Entry Index             |
| 0x18   | 0x8           | Maximum Entry Index, always 16 |
|        |               |                                |

### Mouse Entry

| Offset | Size in bytes | Description                 |
| ------ | ------------- | --------------------------- |
| 0x0    | 0x8           | Timestamp in samples        |
| 0x8    | 0x8           | Timestamp in samples again? |
| 0x10   | 0x4           | Mouse X                     |
| 0x14   | 0x4           | Mouse Y                     |
| 0x18   | 0x4           | Mouse X Change              |
| 0x1C   | 0x4           | Mouse Y Change              |
| 0x20   | 0x4           | Scroll Change Y             |
| 0x24   | 0x4           | Scroll Change X?            |
| 0x28   | 0x8           | Mouse Buttons               |
|        |               |                             |

## Keyboard

| Offset | Size in bytes | Description      |
| ------ | ------------- | ---------------- |
| 0x0    | 0x20          | Keyboard Header  |
| 0x20   | 0x38 \* 17    | Keyboard Entries |
|        |               |                  |

### Keyboard Header

| Offset | Size in bytes | Description                    |
| ------ | ------------- | ------------------------------ |
| 0x0    | 0x8           | Timestamp in ticks?            |
| 0x8    | 0x8           | Number of Entries, always 17   |
| 0x10   | 0x8           | Latest Entry Index             |
| 0x18   | 0x8           | Maximum Entry Index, always 16 |
|        |               |                                |

### Keyboard Entry

| Offset | Size in bytes | Description                                                                                        |
| ------ | ------------- | -------------------------------------------------------------------------------------------------- |
| 0x0    | 0x8           | Timestamp in samples                                                                               |
| 0x8    | 0x8           | Timestamp in samples again?                                                                        |
| 0x10   | 0x8           | Modifier Mask                                                                                      |
| 0x18   | 0x20          | Keys Down, each key gets one bit based on the HID keyboard scan code (F1 is 0x3A, bit 0x3A is set) |
|        |               |                                                                                                    |

## Controller Serials?

This section contains a series of 16 structures 0x400 bytes large.

| Offset | Size in bytes | Description       |
| ------ | ------------- | ----------------- |
| 0x30   | 0xE           | Controller Serial |
| 0x60   | 0xE           | Controller Serial |
|        |               |                   |

## Controllers

This section contains a series of 10 0x5000 byte structures describing
each available controller.

| Controller Index | Description    |
| ---------------- | -------------- |
| 0 to 7           | Players 1 to 8 |
| 8                | Handheld Mode  |
| 9                | Unknown        |
|                  |                |

### Controller

| Offset | Size in bytes            | Description                                                |
| ------ | ------------------------ | ---------------------------------------------------------- |
| 0x0    | 0x28                     | Controller Header                                          |
| 0x28   | 0x20 header + 0x30 \* 17 | Controller Pro Controller State                            |
| 0x378  | 0x20 header + 0x30 \* 17 | Controller Handheld Joined State                           |
| 0x6C8  | 0x20 header + 0x30 \* 17 | Controller Joined State (Lone Joy-Con or Pair of Joy-Con)  |
| 0xA18  | 0x20 header + 0x30 \* 17 | Controller Left State (Vertical Controls w/ Joy-Con Half)  |
| 0xD68  | 0x20 header + 0x30 \* 17 | Controller Right State (Vertical Controls w/ Joy-Con Half) |
| 0x10B8 | 0x20 header + 0x30 \* 17 | Controller Main State (No Analog Sticks)                   |
| 0x1408 | 0x20 header + 0x30 \* 17 | Controller Main State                                      |
| 0x1758 | 0x20 header + 0x68 \* 17 | SixAxisSensor Pro Controller State                         |
| 0x1E60 | 0x20 header + 0x68 \* 17 | SixAxisSensor Handheld State                               |
| 0x2568 | 0x20 header + 0x68 \* 17 | SixAxisSensor Pair Left State                              |
| 0x2C70 | 0x20 header + 0x68 \* 17 | SixAxisSensor Pair Right State                             |
| 0x3378 | 0x20 header + 0x68 \* 17 | SixAxisSensor Single Left State                            |
| 0x3A80 | 0x20 header + 0x68 \* 17 | SixAxisSensor Single Right State                           |
| 0x41D0 | 0x10                     | Controller MAC                                             |
| 0x41F0 | 0x10                     | Controller MAC                                             |
|        |                          |                                                            |

#### Controller Header

| Offset | Size in bytes | Description                                                                                           |
| ------ | ------------- | ----------------------------------------------------------------------------------------------------- |
| 0x0    | 0x4           | Status, bit0 Pro Controller/HID controller, bit1 wired for handheld, bit2 pair, bit3 left, bit4 right |
| 0x4    | 0x4           | Is Joy-Con Half                                                                                       |
| 0x8    | 0x4           | bit1 color set does not exist                                                                         |
| 0xC    | 0x4           | RGBA Body Color (single Joy-Con or Pro Controller)                                                    |
| 0x10   | 0x4           | RGBA Button Color (single Joy-Con or Pro Controller)                                                  |
| 0x14   | 0x4           | bit1 color set does not exist                                                                         |
| 0x18   | 0x4           | RGBA Body Color (right Joy-Con)                                                                       |
| 0x1C   | 0x4           | RGBA Button Color (right Joy-Con)                                                                     |
| 0x20   | 0x4           | RGBA Body Color (left Joy-Con)                                                                        |
| 0x24   | 0x4           | RGBA Button Color (left Joy-Con)                                                                      |
|        |               |                                                                                                       |

#### Controller State Header

| Offset | Size in bytes | Description                    |
| ------ | ------------- | ------------------------------ |
| 0x0    | 0x8           | Timestamp in ticks?            |
| 0x8    | 0x8           | Number of entries, always 17   |
| 0x10   | 0x8           | Latest Entry Index             |
| 0x18   | 0x8           | Maximum Entry Index, always 16 |
|        |               |                                |

#### Controller State

| Offset | Size in bytes | Description                                   |
| ------ | ------------- | --------------------------------------------- |
| 0x0    | 0x8           | Timestamp in samples                          |
| 0x8    | 0x8           | Timestamp in samples again                    |
| 0x10   | 0x8           | Button State                                  |
| 0x18   | 0x4           | Left Joystick X                               |
| 0x1C   | 0x4           | Left Joystick Y                               |
| 0x20   | 0x4           | Right Joystick X                              |
| 0x24   | 0x4           | Right Joystick Y                              |
| 0x28   | 0x8           | Controller State (bit0 connected, bit1 wired) |
|        |               |                                               |

##### Button State

| Bit | Button              |
| --- | ------------------- |
| 0   | A                   |
| 1   | B                   |
| 2   | X                   |
| 3   | Y                   |
| 4   | Left Stick Pressed  |
| 5   | Right Stick Pressed |
| 6   | L                   |
| 7   | R                   |
| 8   | ZL                  |
| 9   | ZR                  |
| 10  | Plus                |
| 11  | Minus               |
| 12  | Left                |
| 13  | Up                  |
| 14  | Right               |
| 15  | Down                |
| 16  | Left Stick Left     |
| 17  | Left Stick Up       |
| 18  | Left Stick Right    |
| 19  | Left Stick Down     |
| 20  | Right Stick Left    |
| 21  | Right Stick Up      |
| 22  | Right Stick Right   |
| 23  | Right Stick Down    |
| 24  | SL                  |
| 25  | SR                  |
|     |                     |

##### SixAxisSensor State Header

| Offset | Size in bytes | Description                   |
| ------ | ------------- | ----------------------------- |
| 0x0    | 0x8           | Timestamp in ticks?           |
| 0x8    | 0x8           | Number of entries, always 17  |
| 0x10   | 0x8           | Latest Entry Index            |
| 0x18   | 0x8           | Maximum Entry Index, up to 16 |
|        |               |                               |

##### SixAxisSensor State Entry

| Offset | Size in bytes | Description                               |
| ------ | ------------- | ----------------------------------------- |
| 0x0    | 0x8           | Timestamp in samples                      |
| 0x8    | 0x8           | Unknown                                   |
| 0x10   | 0x8           | Timestamp in samples again                |
| 0x1C   | 0x4 \* 3      | Accelerometer data as 3 floats            |
| 0x24   | 0x4 \* 3      | Gyroscope data as 3 floats                |
| 0x30   | 0x4 \* 3      | Unknown sensor data as 3 floats           |
| 0x3C   | 0x4 \* 9      | Orientation basis as 3x3 matrix of floats |
| 0x60   | 0x8           | Unknown, always 1                         |

Official sw copies the data from offset 0x8 size 0x60 to the final
output state.
