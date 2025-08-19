ai 를 처리하려면, memory가 필요하다.
- model에서 사용할 메모리
  HD_COMMON_MEM_USER_DEFINIED_POOL, DDR_ID0
  초기에 이 pool을 만들어 놓아야 한다.
- input image를 위한 memory
  data structure: VENDOR_AI_NET_CFG_WORKBUF
  private pool에서 할당.
  VENDOR_AI_NET_PARAM_CFG_WORKBUF id로 가져온 메모리를 세팅.
# Flow
model 하나를 본다면,   
1. load model
2. vendor_ai_net_open
3. input image를 위한 메모리 세팅
4. vendor_ai_net_start
5. proc 반복