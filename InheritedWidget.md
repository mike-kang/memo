# 역할
데이터의 전달. 이 widget은 statelesswidget이나 statefulwidget처럼 build method를 제공하지 않는다. 그리는 것이 목적이 아닌 데이터 전달이 목적이다.
statelesswidget이나 statefulwidget 은 자신이 받은 property 나 자신이 가지고 있는 state 만을 가지고 그림을 그리는 게 한계다. 이 위젯들이 직접 전달 받지 않은 data가지고 그릴 수 있게 하고, 이 data가 변경되었을 때, 자동으로 rebuld되게 하는 것이 inheritedwidget의 목적이다.
# 어떻게 Data 를 전달하나?
트리 상의 하위 위젯들은 buildcontext를 통해,  InheritedWidget의 data에 접근할 수 있다.
```dart
class MyData extends InheritedWidget {
  final int counter;

  const MyData({
    required this.counter,
    required super.child,
  });

  static MyData? of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<MyData>();
  }

  @override
  bool updateShouldNotify(MyData oldWidget) {
    return counter != oldWidget.counter;
  }
}
```
자식 위젯에선
```dart
@override
Widget build(BuildContext context) {
  final counter = MyData.of(context)?.counter ?? 0;

  return Text('Counter: $counter');
}
```


# 자신의 Data를 참조하는 객체들을 Framework은 언제 rebuild 시킬까?
inheritedwidget이 다시 생성될 때. 하지만 이 위젯이 다시 생성 될 때는 많을 것이고, 데이타가 변경되지 않을 때에도 다시 생성될 수 있다. 그래서, updateShouldNotify 라는 함수를 구현하라고 제공해준다.
이 함수가 true를 반환할 때만, data를 참조하는 객체들을 rebuld한다.

# 이 inheritedwidget 자체만으론 property로 받은 데이타를 전달하는 역할만 한다. 이 data를 변경하는 것은 역할 밖이다.
