AE가 LV에 민감하며, AWB는 color temperature에 민감하다.
이 중요 인자인 color temperature에 가중치를 줄 수 있으며, 이 가중치는 in, out, night와 Color Temperature에 의해 결정된다.

| CT    | Out | In  | Night |
|-------|-----|-----|--------|
| 2300  |  1  |  1  |   1    |
| 2800  |  1  |  1  |   1    |
| 3700  |  1  |  1  |   1    |
| 4700  |  1  |  1  |   1    |
| 6500  |  1  |  1  |   1    |
| 11000 |  1  |  1  |   1    |
이 out, in, night는 LV로 결정된다.


| 이름              | 내용                         | in  |
| --------------- | -------------------------- | --- |
| Luminance Value | 외부 빛                       | X   |
| ColorT(K)       | 색온도                        | X   |
| Mode            | 수렴상태<br>(Converge, Adjust) | X   |
| R Gain          | 계산된 Red Gain               | X   |
| G               | 계산된 Green Gain             | X   |
| B               | 계산된 Blue Gain              | X   |
