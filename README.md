**Work-in-Progress** - Initial Layout complete, matched-length traces TODO.

PCI-Express to OpenCAPI SlimSAS 8x Connector Compatible Adapter PCB.

# PCIe-to-SlimSAS8x

The [Open Coherant Accelerator Processor Interface (OpenCAPI)](https://opencapi.org/wp-content/uploads/2022/07/OpenCAPI-Overview.pdf) standard has FPGA-based [Advanced Accelerated Cable (AAC)](https://files.openpower.foundation/s/xSQPe6ypoakKQdq/download/25Gbps-spec-20171108.pdf) [Add-In cards](https://opencapi.org/wp-content/uploads/2018/12/OpenCAPI-Tech-SC18-Exhibitor-Forum.pdf) such as [ADM-PCIE-9H3](https://www.alpha-data.com/product/adm-pcie-9h3/), [ADM-PCIE-9H7](https://www.alpha-data.com/alpha-data-release-adm-pcie-9h7-data-center-board-with-xilinx-virtex-ultrascale-hbm-fpga/), [ADM-PCIE-9V3](https://www.alpha-data.com/product/adm-pcie-9v3/), [ADM-PCIE-9V5](https://www.alpha-data.com/product/adm-pcie-9v5/), [BittWare XUP-VV4](https://www.bittware.com/fpga/xup-vv4/), [BittWare XUP-VVH](https://www.bittware.com/fpga/xup-vvh/), and [Nvidia Innova-2 Flex](https://www.nvidia.com/en-us/networking/ethernet/innova-2-flex/).

The OpenCAPI SlimSAS interface was designed as a low-latency version of [PCI-Express](https://en.wikipedia.org/wiki/PCI_Express) and includes all necessary signals. This project is an attempt to create an adapter capable of connecting to such FPGA boards using PCIe over SlimSAS cables.




# Schematic

![PCIe-to-SlimSAS 8x Schematic](img/PCIe-to-SlimSAS8x_Schematic.png)




# PCB Layout

TODO: Matched-length traces.

4-Layer PCB. Inner 2 layers are GND planes.

![PCIe-to-SlimSAS 8x Layout](img/PCIe-to-SlimSAS8x_Layout.png)




## Design Notes

Refer to the [OpenPower Advanced Accelerated Cable (AAC) Electro-Mechanical Specification](https://files.openpower.foundation/s/xSQPe6ypoakKQdq/download/25Gbps-spec-20171108.pdf).

Only a single component is requred, a [U10A474200T](https://www.digikey.com/en/products/detail/amphenol-cs-commercial-products/U10A474200T/14632855)/[U10A474200T](https://www.digikey.com/en/products/detail/amphenol-cs-commercial-products/U10A474200T/14632855) SlimSAS 8x Right-Angle SMD Connector.




### PCB Stackup and Impedance Control

OpenCAPI uses 85ohm impedance cables.

![85ohm Impedance in KiCad Calculator](img/PCB_85ohm_Impedance_on_0.21mm_PR7628.png)

