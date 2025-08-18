## Description
In versions 0.8.*, The `restart\pause` method of agent-zero is exposed, that unthenticated attackers can restart the system and cause a denial of service.This issue has been fixed in version 0.9
## Environment
- **Operating System** :windows docker
-  **Affected Version** :  0.8.*
-  **Test Date**: 2025/6/20

## PoC
1. visit `http://host/<restart/pause>`

Refresh becomes unresponsive but recovers after some time

## Vulnerable Code Location:  
`/python/api/restart.py`,`/python/api/pause.py`
specifically at: 
```python
process.reload()
```
and
```python
 context.paused = paused
```
