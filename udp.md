## udp socket write시에 block될 수 있나요?
커널은 socket별로 send buf를 관리하고, NIC 별로 송신큐를 관리한다. send buf가 차면, block 될 수 있다.
