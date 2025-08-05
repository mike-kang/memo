언제 사용하나?
  여러 윈도우가 필요한 경우. 내 경우엔 카메라 포커스 맞추는 툴을 만들 때 사용했는데, 처음에는 이 MDI를 사용하지 않고 만들었었다. 문제는 다른 프로그램을 잠깐 사용하고 난 후, 이 Focus app을 사용하려면, 뒤에 있는 여러 창을 일일이 앞으로 나오게 하는 불편함이 있었다.

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

Client window 는 FrameWndProc의 WM_CREATE에서 생성한다.
```c
        CLIENTCREATESTRUCT ccs;
        ccs.hWindowMenu = NULL;
        ccs.idFirstChild = 100;

        hMDIClient = CreateWindow(L"MDICLIENT", NULL,
            WS_CHILD | WS_CLIPCHILDREN | WS_VISIBLE,
            0, 0, 0, 0, hWnd,
            (HMENU)1, hInst, (LPVOID)&ccs);
```

Child Window는 Client window에 WM_MDICREATE 를 보내서 생성한다. 이때, lparam에 MDICREATESTRUCT을 보낸다.
```c
        MDICREATESTRUCT mcs;
        mcs.szClass = L"sub_window";
        mcs.szTitle = L"zoom";
        mcs.hOwner = hInst;

        ScreenToClient(hWnd, &p->lt);  // 클라이언트 영역의 크기

        mcs.x = p->lt.x + p->point.x;
        mcs.y = p->lt.y + p->point.y;
        mcs.cx = MySettings::GetWindowWidth(L"SubWindow");
        mcs.cy = MySettings::GetWindowHeight(L"SubWindow");
        mcs.style = WS_CHILD | WS_VISIBLE | WS_CAPTION | WS_SYSMENU;
        SubWindow* sw = new SubWindow(mcs.cx, mcs.cy, 3.);
        mcs.lParam = (LPARAM)sw;
        HWND hSubWindow = (HWND)SendMessage(hMDIClient, WM_MDICREATE, 0, (LPARAM)&mcs);
```

======================================================
여러 child window를 만들 때, child window의 static winproc에서 어떻게 구분해서 처리할 수 있을까?
winproc는 HWND를 인자로 받는다.  각 윈도우는 자신만의 userdata address 공간을 갖는다.
set : 		SetWindowLongPtr(wnd, GWLP_USERDATA, (LONG_PTR)sw);
get:	    SubWindow* my = (SubWindow*)GetWindowLongPtr(wnd, GWLP_USERDATA);
WndProc의 WM_CREATE에서 set을 한다.

위에  WM_MDICREATE을 보낼 때, mcs.lParam = (LPARAM)sw;
받는 WndProc에서는 아래와 같이 한다.
```c
	case WM_CREATE: 
	{
		LPCREATESTRUCT pcs = (LPCREATESTRUCT)lparam;
		MDICREATESTRUCT* pmcs = (MDICREATESTRUCT*)pcs->lpCreateParams;
		SubWindow* sw = (SubWindow*)pmcs->lParam;
		SetWindowLongPtr(wnd, GWLP_USERDATA, (LONG_PTR)sw);
```