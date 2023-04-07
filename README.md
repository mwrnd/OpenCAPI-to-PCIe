**Work-in-Progress** - Working on Second Revision. I was unable to get the first revision working with the Innova-2. The [OpenPower version of the AAC Spec](https://files.openpower.foundation/s/xSQPe6ypoakKQdq/download/25Gbps-spec-20171108.pdf) I used has a different pinout than the [ADM-PCIE-9V5 User Manual (Pg15-19of38)](https://www.alpha-data.com/xml/user_manuals/adm-pcie-9v5%20user%20manual_v1_4.pdf).

PCI-Express to OpenCAPI-Compatible SlimSAS 8x Adapter PCB.

# PCIe-to-SlimSAS8x

The [Open Coherant Accelerator Processor Interface (OpenCAPI)](https://opencapi.org/wp-content/uploads/2022/07/OpenCAPI-Overview.pdf) standard has FPGA-based [Advanced Accelerated Cable (AAC)](https://files.openpower.foundation/s/xSQPe6ypoakKQdq/download/25Gbps-spec-20171108.pdf) [Add-In cards](https://opencapi.org/wp-content/uploads/2018/12/OpenCAPI-Tech-SC18-Exhibitor-Forum.pdf) such as [ADM-PCIE-9H3](https://www.alpha-data.com/product/adm-pcie-9h3/), [ADM-PCIE-9H7](https://www.alpha-data.com/alpha-data-release-adm-pcie-9h7-data-center-board-with-xilinx-virtex-ultrascale-hbm-fpga/), [ADM-PCIE-9V3](https://www.alpha-data.com/product/adm-pcie-9v3/), [ADM-PCIE-9V5](https://www.alpha-data.com/product/adm-pcie-9v5/), [BittWare XUP-VV4](https://www.bittware.com/fpga/xup-vv4/), [BittWare XUP-VVH](https://www.bittware.com/fpga/xup-vvh/), and [Nvidia Innova-2 Flex](https://www.nvidia.com/en-us/networking/ethernet/innova-2-flex/).

The OpenCAPI SlimSAS interface is based on [PCI-Express](https://en.wikipedia.org/wiki/PCI_Express). This project is an attempt to create an adapter capable of connecting to such FPGA boards using PCIe over SlimSAS cables.




# Schematic

![PCIe-to-SlimSAS 8x Schematic](img/PCIe-to-SlimSAS8x_Schematic.png)




# PCB Layout

4-Layer PCB. Inner 2 layers are GND planes.

![PCIe-to-SlimSAS 8x Layout](img/PCIe-to-SlimSAS8x_Layout.png)




## Design Notes

Refer to the [OpenPower Advanced Accelerated Cable (AAC) Electro-Mechanical Specification](https://files.openpower.foundation/s/xSQPe6ypoakKQdq/download/25Gbps-spec-20171108.pdf).

Only a single component is required, a [U10A474200T](https://www.digikey.com/en/products/detail/amphenol-cs-commercial-products/U10A474200T/14632855)/[U10A474240T](https://www.digikey.com/en/products/detail/amphenol-cs-commercial-products/U10A474240T/17066204) SlimSAS 8x Right-Angle SMD Connector. The two [U.FL](https://www.digikey.com/en/products/detail/hirose-electric-co-ltd/U-FL-R-SMT-1-01/3978494)/[UMCC](https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/1909763-1/4731728) connectors are for test purposes only. 

This is meant to be an early prototype board.

Differential pairs are matched to within 0.5mm intra-pair (N-to-P). Should work at least at [PCIe Gen1](https://www.youtube.com/watch?v=QG0Apol-oj0&t=2832s).


| Diff. Pair | Length (mm) |
| -----------|:-----------:|
| RX0        | 40.2        |
| RX1        | 30.7        |
| RX2        | 34.7        |
| RX3        | 19.8        |
| RX4        | 18.6        |
| RX5        | 30.0        |
| RX6        | 19.2        |
| RX7        | 22.1        |
| TX0        | 35.1        |
| TX1        | 35.5        |
| TX2        | 35.9        |
| TX3        | 26.6        |
| TX4        | 23.0        |
| TX5        | 44.4        |
| TX6        | 38.7        |
| TX7        | 47.2        |


### PCB Stackup

I am using values from [JLCPCB](https://jlcpcb.com/capabilities/pcb-capabilities).

![4-Layer Stackup](img/PCIe-to-SlimSAS8x_Layer_Stackup.png)


### Trace Impedance Control

OpenCAPI uses 85ohm impedance cables. I played with the values until I got the loosest differential pair coupling that is manufacturable with larger tolerances.

![85ohm Differential Impedance in DigiKey Calculator](img/PCB_Impedance_0.30mm_0.18mm_on_0.21mm_7628.png)

The PCB also includes a 45mm long [Microstrip](https://en.wikipedia.org/wiki/Microstrip) trace to test and compare theory to reality.

![Test Microstrip Trace Impedance](img/PCB_Impedance_Microstrip_0.3mm_on_0.21mm_7628.png)

