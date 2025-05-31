std::thread에서 thread를 취소하는 것은 pthread_cancel을 사용할 수 있는데, 이때 native thread_id를 알아야 한다.
이 thread_id는 detach 나 join전에 알아야 한다.
문제는 detach 전에 알아둔 thread_id가 thread가 이미 죽어서, 다른 thread에게 할당되었다면, 문제가 될 수 있다.

결론:
std::thread는 pthread의 wrapper로 native thread_id 는 pthread_t를 뜻하며, 
detach 를 호출할 경우, 더 이상 pthread를 관리하지 않으므로 thread_id 정보가 없다.
