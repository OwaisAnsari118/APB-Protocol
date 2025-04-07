# APB-Protocol
# Why APB?
- Low-cost
- Low-power
- Low-complexity
- Non-pipelined
- Ideal for peripherals
- Single Master/Multiple Slaves
- Multiple Master/Multiple Slaves
  
# Real Life Example.
Actel SmartFusion Soc:
![Screenshot 2025-04-06 211813](https://github.com/user-attachments/assets/6857af87-47a0-4f05-906d-2a62fd0ca195)
Logical view:
![Screenshot 2025-04-04 162523](https://github.com/user-attachments/assets/1a5782c9-8f59-4e90-9fb5-611084e9d65a)

# APB signal definations
| Signal Name | Description                                                   | Per Slave | Source |
|-------------|---------------------------------------------------------------|-----------|--------|
| PCLK        | The bus clock source (rising-edge triggered)                  | No        | System |
| PRESETn     | The bus (and typically system) reset signal (active low)      | No        | System |
| PADDR       | The APB address bus (can be up to 32-bits wide)               | No        | System |
| PSELx       | The select line for each slave device                         | Yes       | Master |
| PENABLE     | Indicates the 2nd and subsequent cycles of an APB transfer    | No        | Master |
| PWRITE      | Indicates transfer direction (Write = 1, Read = 0)            | No        | Master |
| PWDATA      | The write data bus (can be up to 32-bits wide)                | No        | Master |
| PREADY      | Used to extend a transfer                                     | Yes       | Slave  |
| PRDATA      | The read data bus (can be up to 32-bits wide)                 | Yes       | Slave  |
| PSLVERR     | Indicates a tranfer error (OKAY = 0, ERROR = 1)               | Yes       | Slave  |
| PSTRB       | Write strobes. This signal indicates which byte lanes to update during a write transfer. There is one write strobe for each eight bits of the write data bus. Strobe must not be active during read | Yes       | Slave  |
| PPROT       | Protection type. This signal indicates the normal, privileged, or secure protection level of the tansaction and whether the transaction is a data access or an instruction access.   | Yes       | Slave  |

# Protection unit support
| PPROT[2:0] | Protection Level                          |
|------------|-------------------------------------------| 
| [0]        | 1 = Privileged access,  0 = normal access |
| [1]        | 1 = nonsecure access,   0 = secure access |
| [2]        | 1 = instruction access, 0 = data access   |  

# Actel CoreAPB3 - Single Master and Multiple Slaves.
![Screenshot 2025-04-06 231935](https://github.com/user-attachments/assets/ae8fe979-9579-46f6-a678-b1ff53b33a46)
* ARM APB sepcification is silent about multiple slave connection
* Allocates per-slave signals
  - CoreAPB3 support 16 slaves
  - Performs address decoding for PSEL
  - De-multiplexes PSEL signal
  - Multiplexes PREADY, PRDATA, PSLVERR
  - The upper four address bits driven by the master are decoded to produce the select signals for the 16 slave slots, regardless of the master address bus width.

# APB Timing waveform notations
![Screenshot 2025-04-06 233037](https://github.com/user-attachments/assets/52b8052c-ac0a-4f0f-9002-dfdef43bdabe)

# APB State Machine
![Screenshot 2025-04-07 000148](https://github.com/user-attachments/assets/5079f16e-10ad-4752-ad03-8c2d3b0d788e)

