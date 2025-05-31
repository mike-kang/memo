**

Bandwidth and Data Rate

Pixel Clock – 초당 전송되는 pixel 수(Hz)

Bandwidth – the capacity required in Mbps of a given system to pass a specific frequency

Data Rate – the data flow throughput in bits per second of the transport layer

**

Examples

5.2.1. Example 1: 1920x1080p@60Hz, RAW10, 2-lane

Total Horizontal Samples = 2200, Total Vertical Lines = 1125

Pixel Clock Frequency = 2200 x 1125 x 60 = 148.5 MHz

Bandwidth (Total Data Rate) = 148.5 MHz * 10-bit = 1.485 Gbps

Line Rate (Data Rate per Lane) = 1.485 Gbps/2-lane = 742.5 Mbps

 MIPI Bit Clock Frequency = 742.5/2 = 371.25 MHz
==============================================================
IMX 412
3008x3008p@30Hz, RAW10, 4-lane
Total Horizontal Samples = 3194, Total Vertical Lines = 3719
Pixel Clock Frequency  = 3194x3719x30 = 356.4 MHz
Bandwidth (Total Data Rate) = 356.4 MHz * 10bit = 3.564 Gbps
Line Rate (Data Rate per Lane) = 3.564 Gbps/4lane = 890.9MHz

==========================================================
IMX675 (2592 x 1944)
Total Horizontal Samples = 2900, Total Vertical Lines = 2200
Pixel Clock Frequency  = 2900x2200x30 = 191.4 MHz
Bandwidth (Total Data Rate) = 191.4 MHz * 12bit = 2.297 Gbps
Line Rate (Data Rate per Lane) = 2.297 Gbps/4lane = 574.2MHz

In the context of cameras and sensors, ==exposure time and integration time are essentially the same thing==. They both refer to the duration during which a camera's sensor is exposed to light to capture an image. Exposure time is more commonly used in photography, while integration time is often used in scientific and industrial applications. 

Elaboration: 

- **Exposure Time:**
    
    This is the duration a camera's sensor is exposed to light, typically controlled by the shutter speed in photography.
    
- **Integration Time:**
    
    This is the period during which a camera sensor collects and integrates photons (light particles) to form an image.


![[Pasted image 20250507182818.png]]
Rolling shutter는 라인 별로 생각해야 한다.
Readout 의 의미는 output을 보면 알 수 있다.  line을 읽어 전송하는 것.

각 라인 별로 보면 readout이 끝나고 다음번 readout 전에 Integration time이 필요한데, 이 Integration time 전에 delay가 SHR0이다.

Integration time = (1H period) × (1 frame period – SHR0) + Toffset
 SHR0 is the shutter sweep time. 4 to (Number of lines per frame - 1)
 VMAX is 1 frame period.
 Toffset is 0.

Integration time를 조절할 때는, VMAX는 고정하고, SHR0만 조절하거나, VMAX를 조절한다.  
(VMAX를 조절하면 framerate에 영향을 주게 된다.)

