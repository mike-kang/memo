# array

```c++
//{"aaa", "bbb", "ccc"}
  for(auto it = files.begin(); it != files.end(); ++it)
  {
    string key = it->asString();
    QLOGV("set_model_uploaded %s\n", key.c_str());
    if(m_map_ai_net.find(key) != m_map_ai_net.end()){
      std::lock_guard<std::mutex> lock(m_map_ai_net[key]->m_mtx_uploaded);
      //업로드된 상태로 변경
      m_map_ai_net[key]->m_bUploaded = true;
    }
  }
```
## 생성하기
```c++
Json::Value root = Json::arrayValue;
for(auto mp : map_new_models_str){
  root.append(mp.second);
}
```
## 확인
```c++
  auto files = root["files"];
  if(!files.isArray()){
```
# Value
```c++
//{"aaa":10, "bbb":20, "ccc":30}

  for(auto it = models.begin(); it != models.end(); ++it)
  {
	string key = it.key().asString();
	int length = it->asInt();
	QLOGV("models %s : %d\n", key.c_str(), length);
	map_new_models[key] = length;
  }
```