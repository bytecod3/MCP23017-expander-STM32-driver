# MCP23017-expander-STM32-driver
MCP23017 expander driver

## Used MCU
I use the STM32F401CCU6 but this driver is compatible with any other MCU

## Usage
1. Include ```mcp23017.h``` header in your main.c file
```#include "mcp23017.h"```

2. Create the instance for an MCP23017 hardware device. You can create up to 8 devices each with different hardware address
as outlined in the datasheet
```
MCP23017 e1;
MCP23017 e2;

MCP23017_instance expander1 = &e1; // base address 0x20
MCP23017_instance expander2 = &e2; // next address 0x21

```

3. In the main function, initialize the MCP23017 object

```
  // initialise MCP23017
  MCP_initialize(expander1, &hi2c1, 0x20);
````

3. Set the pinmodes for a pin
```

/**
* set pin 15 as output
* The driver will automatically resolve which port this pin belongs to.
* The pins are numbered from 0 to 15
*/

MCP_pinmode(expander1, 15, OUTPUT);

```

4. Drive the pin
```
MCP_write_pin(expander1, 15, HIGH);
```

### Reading the GPIOs
You can configure the pins as inputs also. At the moment this driver allows reading of a single pin and reading of a whole port.

#### To read a single pin
To read a single pin use:
```
uint8_t MCP_read_pin(MCP23017_instance inst, uint8_t pin); // returns a 1 or a 0

```

#### To read the whole port
Since the MCP2317 is 16 bit with 2 ports each 8-bit wide, when reading a port you need to pass the port number you want to read.

```
/***
*port_num should be 0 or 1
* 0 for PORTA
* 1 for PORTB
*
* e.g you can read them and store in a uint8_t array then commbine with bit shifting
**/
uint8_t MCP_read_port(MCP23017_instance inst, uint8_t port_num);

```

#### Features to implement
- Interrupts setting
- Internal pullups




