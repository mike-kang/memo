# 특징
- 선언형 UI이다.
- Widget으로 되어있다.
- Widget은 build()에 의해 다시 생성된다.(기존 것은 제거된다.)
- StatelessWidget, StatefulWidget이 있으며, StatelessWidget은 자신을 rebuild할 수 없다.
  StatefulWidget은 State 객체를 통해, 자신을 rebuild 할 수 있다.
- Flutter에서 `build()` 함수는 **화면을 "그리는 것"이 아니라**,  **"어떤 UI가 보여야 하는지를 선언"**하는 함수입니다.
# 선언형 UI
**"UI는 현재 상태에 따라 어떻게 보여야 하는지를 선언만 한다"**  
즉, **“어떻게 바뀌어야 할지”를 절차적으로 설명하는 게 아니라,  
“이 상태면 이렇게 생긴 UI여야 해”라고 선언하는 방식**입니다.

flutter는 statelessWidget과 statefulWidget를 사용해 선언형 UI를 구현한다. statelessWidget과 statefulWidget은 재료다.
StatefulWidget은 자신이 관리하는 상태가 있으며,  해당 상태 변화에 따라 다시 build한다.
StatelessWidget은 관리하는 상태가 없는 경우에 사용한다. 

# 상태가 변할 때, UI를 다시 그리게 하는 구조는 무엇인가?
- `StatefulWidget` + `setState()`
-  상태 관리 패키지 사용 (예: `Provider`, `Riverpod`, `Bloc`, `GetX`, 등)
- `ValueNotifier` + `ValueListenableBuilder`
- 외부 상태 변화 감지 (`StreamBuilder`, `FutureBuilder` 등)
# 위젯트리와 요소트리
플러터는 내부적으로 위젯 tree에 대한 요소 tree를 가진다. 위젯은 build에 의해 다시 생성되기 때문에 이를 관리할 요소가 필요하다.
상태객체와 요소는 오래 살아남는다.

