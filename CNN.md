https://chatgpt.com/share/68c23a33-4984-8004-b85a-1f9ac757ecff

참고 링크 : http://taewan.kim/post/cnn/

Filter와 kernel은 같은 말이다.
CNN에서 학습 대상은 **Filter Parameter**들이다.
Filter도 channel을 가진다. 이 filter의 channel은 input의 channel을 따른다.
filter의 개수는 (width x height x channel) 의 filter가 몇 개인 지를 뜻하며, output(Feature Map)의 channel 과 동일하다.

위 내용을 그림으로 그리면, 
![[Pasted image 20250911121610.png]]

channel 만큼 다 더하므로 값이 커질 것 같지만, filter의 값이 평균이 0이기 때문에(위 그림은 좀 잘못되어 있다.), 다 더해도 값이 커지지 않는다.
