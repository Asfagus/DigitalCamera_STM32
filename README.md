# Digital Camera with STM32F4 Discovery board
This is a project to create a digital camera with STM32

![picture1](01_doc/pic_all.jpg)

<table>
<tr>
<th width="50%">Link to YouTube</th>
<th width="50%">Link to Design Document</th>
</tr>
<tr>
<td>
<a href="https://www.youtube.com/watch?v=MqtJbraAlOU"><img src="http://img.youtube.com/vi/CgX3bM4v_aU/0.jpg" alt="Link to YouTube Video"></a>
</td>
<td>
<a href="https://www.slideshare.net/TakeshiIwanari/how-to-create-digital-camera-with-stm32f4-discovery-board"><img src="01_doc/DigitalCameraDesignDocument_00.jpg" alt="Link to YouTube Video"></a>
</td>
</tr>
</table>

# Specifications
* Still photo capture
	* Live view (around 20 fps)
	* JPEG (*.jpg)
	* QVGA (320x240)
* Movie record
	* Motion JPEG (*.avi)
	* QVGA (320x240)
	* Around 5 fps
* Playback
	* JPEG (up to 2560x1920)
	* RGB565 (320x240)
	* Motion JPEG (around 10 fps)
* Media
	* SD Card (FAT32 format only?,  8GB ~ 16GB of SD card works well)
* How to Control

<img src=01_doc/pic_control.jpg width=50% height=50%>

# Hardware
## Key Components
* STM32F4 Discovery Board
	* STM32F407 VGT (Cortex-M4), (purchased from 秋月)
* Display module
	* ILI9341 controller, 16-bit parallel I/F, (purchased from aitendo)
* Camera module
	* OV7670 without FIFO

## Hardware Connection

![picture1](01_doc/diagram_hardware.jpg)

## Port assign

![picture1](01_doc/diagram_port.jpg)

# Software
## Software Developement Environment
* IDE: SW4STM32 (System Workbench for STM32)
* STM32 Library: HAL with STM32 CubeMX
* External Library: FreeRTOS, FatFS, LibJPEG

## Software Architecture
![picture2](01_doc/diagram_software.jpg)



# Portmap
```
## IO
PA00 = ROTARY_A (TIM5_CH1)	! pulled-up on board
PA01 = ROTARY_B (TIM5_CH2)
PA02 = USART2 (TX)
PA03 = USART2 (RX)
PA04 = CAMERA_HS(DCMI_HSYNC)
PA05 = SD_CARD(SPI1_SCK)
PA06 = CAMERA_PCLK(DCMI_PIXCK)
PA07 = SD_CARD(SPI1_MOSI)
PA08 = CAMERA_MCLK(MCO1)
PA09 = [VBUS_FS]
PA10 = [OTG_FS_ID]
PA11 = [OTG_FS_DM]
PA12 = [OTG_FS_DP]
PA13 = [SWDIO]
PA14 = [SWCLKDebug]
PA15 = SD_CARD(SPI1_NSS(SW control))

PB00 = N/A
PB01 = N/A
PB02 = [BOOT]
PB03 = [SWO]
PB04 = SD_CARD(SPI1_MISO)
PB05 = N/A
PB06 = CAMERA_D5(DCMI_D5)
PB07 = CAMERA_VS(DCMI_VSYNC)
PB08 = CAMERA_D6(DCMI_D6)
PB09 = CAMERA_D7(DCMI_D7)
PB10 = CAMERA(I2C2_SCL)
PB11 = CAMERA(I2C2_SDA)
PB12 = N/A
PB13 = N/A
PB14 = N/A
PB15 = N/A

PC00 = [OTG_FS_PowerSW]  !Don't use
PC01 = BUTTON1
PC02 = BUTTON2
PC03 = BUTTON3
PC04 = N/A
PC05 = CAMERA_RESET
PC06 = CAMERA_D0(DCMI_D0)
PC07 = CAMERA_D1(DCMI_D1)
PC08 = CAMERA_D2(DCMI_D2)
PC09 = CAMERA_D3(DCMI_D3)
PC10 = [CS43L22_SCLK]   !Don't use
PC11 = CAMERA_D4(DCMI_D4)
PC12 = [CS43L22_SDIN]   !Don't use
PC13 = N/A
PC14 = [OSC32_IN]
PC15 = [OSC32_IN]

PD00 = LCD_D2(FSMC_D2)
PD01 = LCD_D3(FSMC_D3)
PD02 = N/A
PD03 = N/A
PD04 = LCD_RD(FSMC_NOE)
PD05 = LCD_WD(FSMC_NWE)
PD06 = N/A
PD07 = LCD_CS(FSMC_NE1)
PD08 = LCD_D13(FSMC_D13)
PD09 = LCD_D14(FSMC_D14)
PD10 = LCD_D15(FSMC_D15)
PD11 = LCD_RS(FSMC_A16)
PD12 = LED
PD13 = LED
PD14 = LED,  LCD_D0(FSMC_D0)
PD15 = LED,  LCD_D1,(FSMC_D1)

PE00 = [LIS302DL_INT1]  !Don't use
PE01 = [LIS302DL_INT2]  !Don't use
PE02 = [LIS302DL_CS]    !Always HIGH
PE03 = N/A
PE04 = N/A
PE05 = N/A
PE06 = N/A
PE07 = LCD_D4(FSMC_D4)
PE08 = LCD_D5(FSMC_D5)
PE09 = LCD_D6(FSMC_D6)
PE10 = LCD_D7(FSMC_D7)
PE11 = LCD_D8(FSMC_D8)
PE12 = LCD_D9(FSMC_D9)
PE13 = LCD_D10(FSMC_D10)
PE14 = LCD_D11(FSMC_D11)
PE15 = LCD_D12(FSMC_D12)


## Function
USART2 = TERMINAL
SPI1   = SD CARD
I2C2   = CAMERA(OV7670)
FSMC   = LCD(ILI9341)
DCMI   = CAMERA(OV7670)
TIMER5_CH1/2 = Rotary Encoder

## DMA
DMA1_5 = USART2_RX
DMA2_1 = CAMERA(DCMI->FSMC(LCD))

## OSC
PH0 = OSC_IN   (external 8MHz)
PH1 = OSC_OUT  (external 8MHz)

## Note
LCD_RESET    = VDD
CAMERA_PWDN  = GND
```
