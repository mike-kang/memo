```c
#include <syslog.h>
syslog(LOG_INFO|LOG_LOCAL0, "switching nv by upload firmware is success!\n", ret);
```
or

```shell
logger -p local0.info -t update "upload success!! $CWD"
```

설정파일: syslogd.conf
```
local0.*   /mnt/app/log
local1.*   /mnt/app/log_cs
```

