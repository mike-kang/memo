크게 Frame window, Client window, child window로 나눠진다.
족보는 아래와 같다.  Frame window가 할아버지 격이다.
Frame window <---- Client window <----child window

Frame window 는 아래와 같이 일반 윈도우 처럼, window class를 만들어 등록해야 한다.
```c
    WNDCLASS wc = { 0 };
    wc.lpfnWndProc = FrameWndProc;
    wc.hInstance = hInstance;
    wc.lpszClassName = L"MDIFrameClass";
    RegisterClass(&wc);
```

Client window 는 FrameWndProc의 WM_CREATE에서
