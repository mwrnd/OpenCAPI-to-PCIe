**Work-in-Progress** - Third Revision design under way. [Second Revision](https://github.com/mwrnd/OpenCAPI-to-PCIe/releases/tag/v0.2-alpha) is being tested. PCIe x8 using the OpenCAPI connector works but requires a high quality cable and uses a PCIe Lane to Transceiver Channel ordering that Vivado complains about.




# PCIe to OpenCAPI-Compatible SlimSAS8x

The [Open Coherant Accelerator Processor Interface (OpenCAPI)](https://opencapi.org/wp-content/uploads/2022/07/OpenCAPI-Overview.pdf) [was a standard](https://opencapi.org/2022/08/09/cxl-consortium-and-opencapi-consortium-sign-letter-of-intent-to-transfer-opencapi-specifications-to-cxl/) that had FPGA-based [Advanced Accelerated Cable (AAC)](https://files.openpower.foundation/s/xSQPe6ypoakKQdq/download/25Gbps-spec-20171108.pdf) [Add-In cards](https://opencapi.org/wp-content/uploads/2018/12/OpenCAPI-Tech-SC18-Exhibitor-Forum.pdf) such as [ADM-PCIE-9H3](https://www.alpha-data.com/product/adm-pcie-9h3/), [ADM-PCIE-9H7](https://www.alpha-data.com/alpha-data-release-adm-pcie-9h7-data-center-board-with-xilinx-virtex-ultrascale-hbm-fpga/), [ADM-PCIE-9V3](https://www.alpha-data.com/product/adm-pcie-9v3/), [ADM-PCIE-9V5](https://www.alpha-data.com/product/adm-pcie-9v5/), [BittWare XUP-VV4](https://www.bittware.com/fpga/xup-vv4/), [BittWare XUP-VVH](https://www.bittware.com/fpga/xup-vvh/), and [Nvidia Innova-2 Flex SmartNIC](https://www.nvidia.com/en-us/networking/ethernet/innova-2-flex/).

The OpenCAPI SlimSAS interface is based on [PCI-Express](https://en.wikipedia.org/wiki/PCI_Express). This project is an attempt to create an adapter capable of connecting to such FPGA boards using PCIe over SlimSAS cables.

![OpenCAPI-to-PCIe Board](img/OpenCAPI-to-PCIe.jpg)

A third revision of the OpenCAPI-to-PCIe is currently being designed to improve signal integrity and reorder the PCIe Lane to Transceiver Channel ordering to avoid Vivado warnings.

![Vivado Critical Warning about Lane Ordering](img/Overriding_Physical_Property_Critical_Warning_Message.png)




## Testing

The [innova2_xdma_opencapi](https://github.com/mwrnd/innova2_xdma_opencapi) project is designed to test the OpenCAPI-to-PCIe Adapter using an [Innova2 Flex SmartNIC](https://github.com/mwrnd/innova2_flex_xcku15p_notes).

Using a [3M 8ES8-1DF21-0.75](https://www.trustedparts.com/en/search/8ES8-1DF21-0.75) cable:

![System with 3M 8ES8-1DF21-0.75 Cable](img/innova2_xdma_opencapi_with_3M_8ES8-1DF21-0.75_Cable.jpg)

PCIe Link Status is usually excellent:

![lspci Link Status](img/lspci_XDMA_OpenCAPI_x8_with_3M_8ES8-1DF21-0.75_Cable.png)

Using an [SFPCables.com SFF-8654 to SFF-8654 8i](https://www.sfpcables.com/24g-internal-slimsas-sff-8654-to-sff-8654-8i-cable-straight-to-90-degree-left-angle-8x-12-sas-4-0-85-ohm-0-5-1-meter) cable:

![System with SFPCables SFF-8654 8i 85Ohm Cable](img/innova2_xdma_opencapi_with_SlimSAS_SFF-8654_8i_85Ohm_Cable.jpg)

PCIe Link Status is downgraded:

![lspci Link Status](img/lspci_XDMA_OpenCAPI_x8_with_SlimSAS_SFF-8654_8i_85Ohm_Cable.png)

I am working on a third revision of the OpenCAPI-to-PCIe adapter to improve signal integrity.




### Additional OpenCAPI Signals

Additional useful signals from the OpenCAPI connector are routed to a 6x1 0.1" Header. The pinout matches a [TC74 I2C Temperature Sensor](https://www.microchip.com/en-us/product/tc74). Note 3.3V is from the PCIe connector. **PRE** is a Presence Detect pin which is connected to GND via a 50-Ohm resistor on the OpenCAPI AAC Add-In card. **RST** is connected to PCIe RESET and OpenCAPI reset.

![TC74A0-3.3VAT in OpenCAPI-to-PCIe Adapter](img/TC74A0-3.3VAT_in_OpenCAPI-to-PCIe_Adapter.jpg)

The [innova2_xdma_opencapi](https://github.com/mwrnd/innova2_xdma_opencapi) project has the ability to test a TC74 in a OpenCAPI-to-PCIe Adapter.

![TC74A0-3.3VAT Testing in a System](TC74A0-3.3VAT_in_OpenCAPI-to-PCIe_Adapter_In-System.jpg)




## PCB Layout

4-Layer PCB. Inner 2 layers are GND planes. Differential pairs are matched to a length of 65mm +/- 1mm both inter-pair and intra-pair (N-to-P).

![OpenCAPI to PCIe x8 PCB Layout](img/OpenCAPI-to-PCIe_PCB_Layout.png)




## Schematic

![OpenCAPI to PCIe x8 Schematic](img/OpenCAPI-to-PCIe_Schematic.png)




## Design Notes

Refer to the [ADM-PCIE-9V5 User Manual (Pg15-19of38)](https://www.alpha-data.com/xml/user_manuals/adm-pcie-9v5%20user%20manual_v1_4.pdf) for the OpenCAPI pinout. Useful [High Speed Design presentation](https://www.youtube.com/watch?v=QG0Apol-oj0&t=2832s).

Only a single component is required for the adapter, a [U10A474200T](https://www.digikey.com/en/products/detail/amphenol-cs-commercial-products/U10A474200T/14632855)/[U10A474240T](https://www.digikey.com/en/products/detail/amphenol-cs-commercial-products/U10A474240T/17066204) SlimSAS 8x Right-Angle SMD Connector. A SlimSAS 8x Cable is required to use the adapter with an OpenCAPI FPGA Board.




### PCB Stackup

I am using values from [JLCPCB](https://jlcpcb.com/capabilities/pcb-capabilities).

![4-Layer Stackup](img/Layer_Stackup.png)




### Trace Impedance Control

OpenCAPI uses 85ohm impedance cables. I played with the values until I got the loosest differential pair coupling that is manufacturable with larger tolerances.

![85ohm Differential Impedance in DigiKey Calculator](img/PCB_Impedance_0.30mm_0.18mm_on_0.21mm_7628.png)




