#### http://127.0.0.1:4242
```sh
ps -ax | grep opentsdb
kill -9 (PID)
cd /usr/local/data/hbase-1.1.2/bin/
./stop-hbase.sh
source /etc/profile
./start-hbase.sh
cd /usr/local/opentsdb/
./build/tsdb tsd --port=4242 --staticroot=build/staticroot --cachedir=/usr/local/data --auto-metric
```

#### 연습 1

```sh
   # 20초마다 100을 openTSDB에 저장하세요
   # 메트릭 이름 변경(원하는 메트릭을 정하세요(예: cc_100))
```

#### 연습 1 결과
```sh
  import time	
  import requests
  import json
  import sys
  import urllib2
  from datetime import datetime, timedelta

  url = "http://127.0.0.1:4242/api/put"

  data = {
      "metric": "cc.inha",
      "timestamp": time.time(),
      "value": 1++,
      "tags": {
         "host": "mypc"
      }
  }

  while 1 :
      t = time.localtime()
      tsec = t.tm_sec
      if tsec%20!=0 :
              print tsec
              time.sleep(0.2)

      else :
	        print "%d 100" % (tesec)
          ret = requests.post(url, data=json.dumps(data))
          time.sleep(0.1)
```


#### exercise 1
   - 주기적으로 증가하는 데이터를 출력

```sh
vim test.py
```

```sh

#!/usr/bin/python
# -*- coding: utf-8 -*- 

count = 0

if __name__ == '__main__':

	while 1 :
		t = time.localtime()
		tsec = t.tm_sec
		
		if tsec%10!=0 :
			print tsec
			time.sleep(0.8)
		else :
			print count
	
```
   
#### exercise 2
   - 주기적으로 증가한는 데이터를 openTSDB에 저장
   - 
   
#### exercise 1,2 결과
```sh
#!/usr/bin/python

import time
import requests
import json
import sys
import urllib2
import time
from datetime import datetime, timedelta

count = 0

url = "http://127.0.0.1:4242/api/put"

while 1 :
    t = time.localtime()
    tsec = t.tm_sec
    if tsec%10!=0 :
            print tsec
            time.sleep(0.2)

    else :
        count = count + 1
        print count
        data = {
    	    "metric": "cc.inha",
            "timestamp": time.time(),
            "value": count,
            "tags": {
            "host": "mypc"
            }
        }
     
        ret = requests.post(url, data=json.dumps(data))
        time.sleep(0.1)
```
