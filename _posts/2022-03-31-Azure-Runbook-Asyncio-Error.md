---
layout: post
title: Azure Runbook Asyncio Error
---
We recently had a project that required the use of Azure runbook. I found my Python code was not working as expected. It works locally but not in Azure runbook.

After debugging, I found the issue is related to Asyncio. Even if I ran the following sample code,I still got an error.

```python
import asyncio
loop = asyncio.get_event_loop()
```

The error message:

```python
**Traceback (most recent call last):  File "C:\Temp\vls2h0kl.4gk\04a596c9-5b8c-4a2d-828b-2bb185668277", line 53, in <module>    loop = asyncio.ProactorEventLoop()  File "C:\WPy64-3800\python-3.8.0.amd64\lib\asyncio\windows_events.py", line 310, in __init__    super().__init__(proactor)  File "C:\WPy64-3800\python-3.8.0.amd64\lib\asyncio\proactor_events.py", line 629, in __init__    self._make_self_pipe()  File "C:\WPy64-3800\python-3.8.0.amd64\lib\asyncio\proactor_events.py", line 760, in _make_self_pipe    self._ssock, self._csock = socket.socketpair()  File "C:\WPy64-3800\python-3.8.0.amd64\lib\socket.py", line 597, in socketpair    lsock.listen()OSError: [WinError 10050] A socket operation encountered a dead networkException ignored in: <function BaseEventLoop.__del__ at 0x0000000784F8C310>Traceback (most recent call last):  File "C:\WPy64-3800\python-3.8.0.amd64\lib\asyncio\base_events.py", line 648, in __del__  File "C:\WPy64-3800\python-3.8.0.amd64\lib\asyncio\proactor_events.py", line 684, in close  File "C:\WPy64-3800\python-3.8.0.amd64\lib\asyncio\proactor_events.py", line 752, in _close_self_pipeAttributeError: 'ProactorEventLoop' object has no attribute '_ssock'**
```

I raised a ticket to Azure Team. I was told it is because Azure runbook only allows on 31 kernel calls and this module seems to be using something out of this range hence getting this error. 

Their product team is working on enabling full stack of OS calls from Azure runbook but it will be delivered for Python by end of 2022. 

So, the temporary workaround is customer can use hybrid runbook worker as of now. 

[Azure Automation Hybrid Runbook Worker overview](https://docs.microsoft.com/en-us/azure/automation/automation-hybrid-runbook-worker)