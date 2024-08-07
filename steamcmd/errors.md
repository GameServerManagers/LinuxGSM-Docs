---
description: Common
---

# Error Codes

## SteamCMD

SteamCMD can sometimes output errors when something goes wrong. Sadly Valve has never released an official list of what the error messages mean. Because of this, a lot of guesswork has been needed to figure it out. This page will highlight what we already know and info on researching what the error might mean in the hope that you can contribute to understanding SteamCMD errors.

SteamCMD uses hexadecimal numbers to give its current "state". Every time SteamCMD does something it changes its state. When SteamCMD fails it will output its has hexadecimal state, for example `0x202`.

## Codes

### Error 0x10E

Seems to affect HLDS based servers. Running again often fixes the issue

```text
Error! App '90' state is 0x10E after update job.
```

| Reason             | Error! App '90' state is 0x10E after update job. |
| ------------------ | ------------------------------------------------ |
| Hex                | 0x10E                                            |
| Decimal/StateFlags | 270                                              |

{% file src="../.gitbook/assets/content_log_0x10E.txt" %}

### Error 0x202

Not enough disk space.

```text
Error! App '<appid_number>' state is 0x202 after update job.
```

| Reason             | Not enough disk quota |
| ------------------ | --------------------- |
| Hex                | 0x202                 |
| Decimal/StateFlags | 514                   |

{% file src="../.gitbook/assets/content_log_0x202.txt" %}

### Error 0x206

{% hint style="info" %}
Unknown error, if you have any details please let us know
{% endhint %}

```text
Error! App '<appid_number>' state is 0x206 after update job.
```

|                    |       |
| ------------------ | ----- |
| Reason             |       |
| Hex                | 0x206 |
| Decimal/StateFlags | 518   |

{% hint style="warning" %}
Missing content_log.txt if you have experienced this error and have a log please let us know.
{% endhint %}

### Error 0x212 [error-0x206](#error-0x206)

Not enough disk space.

```text
Error! App '<appid_number>' state is 0x212 after update job.
```

| Title              | Title                 |
| ------------------ | --------------------- |
| Reason             | Not enough disk space |
| Hex                | 0x212                 |
| Decimal/StateFlags | 530                   |

{% file src="../.gitbook/assets/content_log_0x212.txt" %}

### Error 0x402

Connection issue with steam, you will need to wait for the steam servers to recover.

```text
Error! State is 0x402 after update job.
```

| Reason             | Connection issue |
| ------------------ | ---------------- |
| Hex                | 0x402            |
| Decimal/StateFlags | 1026             |

{% hint style="warning" %}
Missing content_log.txt if you have experienced this error and have a log please let us know.
{% endhint %}

### Error 0x602

{% hint style="info" %}
Unknown error, if you have any details please let us know
{% endhint %}

```text
Error! State is 0x602 after update job.
```

|                    |       |
| ------------------ | ----- |
| Reason             |       |
| Hex                | 0x602 |
| Decimal/StateFlags | 1538  |

{% hint style="warning" %}
Missing content_log.txt if you have experienced this error and have a log please let us know.
{% endhint %}

### Error 0x606

SteamCMD is unable to write to the disk. Normally caused by permissions issues. This issue was discovered when a directory that was linked using symlink did not have the correct permissions to allow SteamCMD to write to it.

```text
Error! App '<appid_number>' state is 0x606 after update job.
```

|                    |                    |
| ------------------ | ------------------ |
| Reason             | Disk write failure |
| Hex                | 0x606              |
| Decimal/StateFlags | 1542               |

{% file src="../.gitbook/assets/content_log_0x606.txt" %}

### Error 0x626

Missing update files

```text
Error! App '232250' state is 0x626 after update job.
```

|                    |                      |
| ------------------ | -------------------- |
| Reason             | Missing update files |
| Hex                | 0x626                |
| Decimal/StateFlags |                      |

{% file src="../.gitbook/assets/content_log_0x626.txt" %}

### Error 0x2

```text
Error! App '<appid_number>' state is is 0x2 after update job.
```

| Reason             |     |
| ------------------ | --- |
| Hex                | 0x2 |
| Decimal/StateFlags | 2   |

{% hint style="warning" %}
Missing content_log.txt if you have it please let us know.
{% endhint %}

### Error 0x6

No connection to content servers.

```text
Error! App '<appid_number>' state is 0x6 after update job.
```

| Reason             | No connection to content servers                       |
| ------------------ | ------------------------------------------------------ |
| Reason 2           | Received 401 (Unauthorized) HTTP response for depot 11 |
| Hex                | 0x6                                                    |
| Decimal/StateFlags | 6                                                      |

{% file src="../.gitbook/assets/content_log_0x6.txt" %}

{% file src="../.gitbook/assets/content_log_0x6-2 (1) (1).txt" %}

### 0x3

```text
Update state (0x3) reconfiguring, progress: 0.00 (0 / 0)
```

### 0x5

```text
Update state (0x5) validating, progress: 13.48 (1554089956 / 11530459441)
```

### 0x11

```text
Update state (0x11) preallocating, progress: 8.53 (983870089 / 11530459441)
```

### 0x61

```text
Update state (0x61) downloading, progress: 1.11 (127644881 / 11530459441)
```

### 0x101

```text
 Update state (0x101) committing, progress: 3.43 (395043827 / 11530459441)
```

## SteamCMD Logs

To get more info and output see the SteamCMD logs in `~/.local/share/Steam/logs`or `~/.steam/logs`. The most useful log is `content_log.txt` that will provide more information on errors.

{% hint style="success" %}
If you have experienced an error we don't have logs for please provide them to us to assist in diagnosing the issue.
{% endhint %}

## SteamCMD Hex Codes

SteamCMD uses hex error codes such as `0x202` which can be converted into decimal `514`. You can use a hex-to-decimal converter to do this. Using the table below you can work out the status messages. By doing a calculation. Find the highest number below the state `512` which is the first error. Then take the number away from the total `514-512=2` which gives you the last error. This can be done for any error

`514-512-2=0`

`512 StateUpdateRunning` , `2 StateUpdateRequired`

| StateInvalid        | 0       |
| ------------------- | ------- |
| StateUninstalled    | 1       |
| StateUpdateRequired | 2       |
| StateFullyInstalled | 4       |
| StateEncrypted      | 8       |
| StateLocked         | 16      |
| StateFilesMissing   | 32      |
| StateAppRunning     | 64      |
| StateFilesCorrupt   | 128     |
| StateUpdateRunning  | 256     |
| StateUpdateRunning  | 512     |
| StateUpdateStarted  | 1024    |
| StateUninstalling   | 2048    |
| StateBackupRunning  | 4096    |
| StateReconfiguring  | 65536   |
| StateValidating     | 131072  |
| StateAddingFiles    | 262144  |
| StatePreallocating  | 524288  |
| StateDownloading    | 1048576 |
| StateStaging        | 2097152 |
| StateCommitting     | 4194304 |
| StateUpdateStopping | 8388608 |

This table is from 2015 and is probably outdated now but it's the best we currently have.

{% embed url="https://github.com/lutris/lutris/blob/master/docs/steam.rst" %}

## ulimit SteamCMD startup error

```text
./steamcmd.sh: line 17: ulimit: open files: cannot modify limit: Operation not permitted
```

Some users may get a ulimit error (no permission/cannot open file) while SteamCMD is starting up. This error caused by a low setting of the -n parameter (number of file descriptors) of ulimit. Some servers forbid increasing ulimit values after startup (or beyond a limit set by root). This can be fixed by changing the file descriptor number ulimit:

```bash
ulimit -n 2048
```

## ERROR! Failed to install app '\<appid_number>' (No subscription)

The Steam account being used does not have a license for the required game.

## ERROR! Password check for AppId \<appid_number> returned error Failure

The password for the branch is incorrect.

## \[S_API FAIL] SteamAPI_Init() failed; SteamAPI_IsSteamRunning() failed

Ignore the error, do not do anything to attempt to fix it. It is a known error that has appeared ever since SteamPipe was introduced. It does not cause any issues and can be ignored.

## Loading Steam API...Failed to init SDL priority manager: SDL not found

Ignore the error, do not do anything to attempt to fix it. It does not cause any issues and can be ignored.

## CWorkThreadPool::\~CWorkThreadPool: work processing queue not empty: 2 items discarded

Ignore the error, do not do anything to attempt to fix it. It does not cause any issues and can be ignored.

## Failed to set thread priority: per-thread setup failed

Ignore the error, do not do anything to attempt to fix it. It does not cause any issues and can be ignored.
