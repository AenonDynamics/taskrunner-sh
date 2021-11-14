## PRELIMINARY ##

### 1.0.0 ###

* Added: simple test scripts
* Changed: `bash` runtime required due to `pipefail` options
* Changed: stdout+stderr of wrapped process are forwarded to stdout
* Changed: command output is stored into temp file

### 0.6.0 ###

* Changed: removed hostname from journalctl output

### 0.5.0 ###

* Added: `taskrunner-systemd` to transmit journald output after unit has been executed

### 0.4.0 ###

* Bugfix: Default exit code `0` in case task has been completed without errors
