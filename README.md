# CakeCraft-WebConsole
Project for Spiralio's minecraft server "CakeCraft SMP Season 2"
## Goals to complete(Server):
- HTTP Python API server on Flask.
  * Create server with one html page.
  * Figure out how to get POST or GET data.
  * Make simple HTTP-request system.
  * Create no-https protection (using md5, secret key, etc.).
- API Base.
  * Create API-request class.
  * Make simple API-method using C++(boost/python.hpp) + Python.
- Backups.
  * Make auto-backup system.
  * Make check hash on backup.info method, so you'll know if backup is modified.
  * Make search by hash or timestamp.
  * Plug in API.
- RCON.
  * Make system to send commands to minecraft server.
  * Figure out how to get console history.
  * Plug in API.
- System statistics.
  * Figure out how to get info:
    - RAM usage.
    - CPU usage.
    - Disk usage.
  * Plug in API.
- Server manipulations.
  * Figure out how to run server remotely.
  * Plug in API.
## Goals to complete(Client):
- HTTP-requests to API by js.
- Simple(at first) html+js web-console.
## Completed(Server):
- HTTP Python API server on Flask.
  * Created server with one html page.
  * Figured out how to get POST or GET data.
  * Make simple HTTP-request system.
- API Base.
  * Create API-request class.
## Completed(Client):
...
## Comments:
- To configure server use server/setup.sh (run in Server directory!).
- To launch server type:
```bash
cd server
./run.sh development #or production
```
Ctrl+C to exit.
## TODO:
- Exception handlers.
## API Methods:
To call methods use:
http://IP:port/method/**METHOD_NAME**?secret=**SECRET**&arg1=val1&arg2=val2&...&argN=valN,
where **SECRET** is md5(secret_key+":"+arg1+"="+val1+","+arg2+"="+val2+","+...+argN+valN+".")
### **stats.get_ram_usage**: returns RAM usage. Arguments:

| argument |   value  | description         |
|:--------:|:--------:|:-------------------:|
|  format  |  percent | in percents         |
|          | fraction | as decimal fraction |

### **stats.get_cpu_usage**: returns CPU usage. Arguments:

| argument |   value  | description         |
|:--------:|:--------:|:-------------------:|
|  format  |  percent | in percents         |
|          | fraction | as decimal fraction |

### **stats.get_disk_usage**: return Disk usage. Arguments:

| argument |   value  | description         |
|:--------:|:--------:|:-------------------:|
|  format  |  percent | in percents         |
|          | fraction | as decimal fraction |

### **rcon.exec_command**: executes command on the server. Also returns console response. Arguments:

| argument | description |
|:--------:|-------------|
| command | Command to execute |

### **rcon.get_history**: returns console history. Arguments:

| argument | description |
|:--------:|-------------|
| count | Amount of lines to return, if 0 - whole history |
| offset | Offset from last line, 0 by default |

### **backup.make**: makes a backup of the important files. Arguments:

| argument | description |
|:--------:|-------------|
| name | Short name of backup, backup_%S_%M_%H_%d_%m by default |
| desc | Full desctiption of backup, empty by default |

### **backup.info**: returns info about backup by timestamp, or the beginning of name or full name . Arguments:
| argument | description |
|:--------:|-------------|
| backup | Timestamp of when backup made, or the beginning of name or full name of backup |

### **backup.list**: returns a list of backups. Arguments:

| argument | description |
|:--------:|-------------|
| count | Amount of backups to return(from the newest one), if 0 - whole list of backups |
| from | Timestamp down to which backups will be displayed, 0 by default, cannot be used with from_name |
| to | Timestamp up to which backups will be displayed, current time by default, cannot be used with to_name |
| from_name | The beginning of name or full name down to which backups will be displayed, optional, cannot be used with from |
| to_name | The beginning of name or full name up to which backups will be displayed, optional, cannot be used with to |


### **backup.switch_to**: saves current files to new backup, and then restore everything to past backup. Arguments:

| argument | description |
|:--------:|-------------|
| backup | Timestamp of when backup made, or the beginning of name or full name of backup |

**WARNING: stop the server before it.**
