Expect luminance (영상의 목표 밝기)를 만들기 위해, sensor gain, shutter speed를 조절

1. Expect luminance 를 고정해도 좋지만, 주변광(LV)에 따라 약간씩 조절하고 싶은 경우를 위해, Novatek은 Expect Luminance Adjustment Table을 만들었다.(LV에 따른 Expect luminance 적용 비율) LV가 3일 때, 50%만 적용하고 싶다면, 이를 조절하면 된다.
2. 


## Auto Low Light(ALL)
exposure time과 framerate는 관련이 있다. exposure time이 1/fps 보다 짧아야지 framerate가 유지된다.
novatek에서는 auto exposure 세팅 시, 저조도에서 exposure time이 길어질 경우, exposure time이 framerate를 유지하는 정도에서 변경할 지, 아니면 더 길게 설정할 수 있는지, Auto Low Light(ALL)로 설정한다. 
ALL가 on이면 더 길게 설정할 수 있게 된다. 이때, 길게 되는 한계는 Max ExpT를 따른다.

exposure time을 표현할 때는 두 가지 방식이 있다.
보통 시간으로 us 단위로 나타내지만, framerate 를 사용해서 표현하기도 한다. 노바텍에서는 exposure time에 us 단위의 시간을 사용하고, Max ExpT에 framerate를 사용해 표현한다. framerate을 사용할 때에는 100 배를 사용하며(초 당이 아닌 100초 framerate), 30fps가 3000 이 된다.
이는 시간으로 나타내면, 3000 -> 1/30s -> 33333us 이다.
   

| 이름              | 내용                                                                                        | 출력  | 입력  | Range    |
| --------------- | ----------------------------------------------------------------------------------------- | --- | --- | -------- |
| Luminance Value | 외부빛                                                                                       | O   | X   |          |
| ISO Cal. Ceof   | 실제 외부 빛이 Luminance Value로 표현될 때, 이 값을 이용해 조절한다.                                           | O   | O   | 0-1023   |
| Exposure Time   | 노출시간                                                                                      | O   | X   |          |
| ISO Gain        | 센서게인                                                                                      | O   | X   |          |
| Lum             | 영상(외부 빛 + 노출시간 + 센서게인)의 밝기<br>(Expect Lum에 수렴)                                            | O   | X   |          |
| ADJ State       | Expect Lum으로 진행하는 상태<br>(Coarse, Stable  2 가지)                                            | O   | X   |          |
| Expect Lum      | 영상 목표 밝기                                                                                  | O   | O   | 0-255    |
| Power Freq      | 50, 60Hz                                                                                  | O   | O   |          |
| Auto Low Light  | enable 일 경우, 설정된 framerate보다 더 긴 노출이 가능하다.<br>(enable, false)                             | O   | O   |          |
| Max ExpT        | Auto Low Light가 enable일 경우에 사용되는 값으로, 설정 가능한 가장 긴 노출 시간으로 us가 아닌, 100초당 가능한 frame수를 설정한다. | O   | O   | 100-6000 |


