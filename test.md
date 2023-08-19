# Test

## publish

> delete build/  (better will add clean command in setup.py)
> python setup.py sdist bdist_wheel
> pip install twine
> twine upload dist/*


## install

> one upload the version
> install that version
    > pip3 install pyhive6si==version
    > pip3 install thrift


## python repl

> install first using above step

```python
## current working directory should be Pyhive root
from pyhive import hive
import inspect
import time
# add new args - just to check if we are using right version or add a VAR
inspect.signature(hive.Connection) 
host = 'define host' # hive-hiveserver2.{env}.6si.com, hive-hiveserver2-adhoc
connection_timeout= 10  # 10 sec
query_timeout = 60  # 60 sec
conn = hive.connect(host=host, port=10000, username='hadoop',database='default', auth='NOSASL', configuration={}, connection_timeout_ms=connection_timeout * 1000, query_timeout_ms=query_timeout * 1000)
time.sleep(connection_timeout)
curr = conn.cursor()
curr.execute("select count(*) from abhishek.unified_events")
a = curr.fetchone()
time.sleep(query_timeout_ms)
curr.execute("select dt, count(*) from abhishek.unified_events group by dt"")
curr.description
a = curr.fetchall()
curr.fetch_logs()
conn.close()
```
