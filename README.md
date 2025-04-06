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
| PSTRB       | Write strobes. This signal indicates which byte lanes to update during a write transfer. There is one write strobe for each eight bits of the write data bus. Strobe must not be active during read                               | Yes       | Slave  |



