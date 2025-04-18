exposure time과 framerate는 관련이 있다. exposure time이 1/fps 보다 짧아야지 framerate가 유지된다.
novatek에서는 auto exposure 세팅 시, 저조도에서 exposure time이 길어질 경우, exposure time이 framerate를 유지하는 정도에서 변경할 지, 아니면 더 길게 설정할 수 있는지, Auto Low Light로 설정한다. 
ALL가 on이면 더 길게 설정할 수 있게 된다. 이때, 길게 되는 한계는 Max ExpT를 따른다.

exposure time을 표현할 때는 두 가지 방식이 있다.
보통 시간으로 us 단위로 나타내지만, framerate 를 사용해서 표현하기도 한다. 노바텍에서는 exposure time에 us 단위의 시간을 사용하고, Max ExpT에 framerate를 사용해 표현한다. framerate을 사용할 때에는 100 배를 사용하며, 30fps가 3000 이 된다.
이는 시간으로 나타내면, 3000 -> 1/30s -> 33333us 이다.
   

exposure time을 결정할 때, encoder의 frame rate에 의해 계산된 1/frame rate 보다 길어지면,  frame rate 이 떨어진다. 이를  