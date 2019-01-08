taskrunner-sh
=============================

**Centralized logging of cron and backup tasks without the need of host-based smtp transport/sendmail**

captures the command output and send it via `http post` to a custom REST endpoint to aggregate data (e.g. cron, backups)

## Architecture ##

TBD

## Usage ##

```bash
# print "1234" to stdout via "echo" - identified as "my-task-name"
taskrunner "my-task-name" echo "1234"
```

## Cron Examples ##

the output/logs of `rsnapshot` will be aggregated

```bash
# backup daily - 6:50
50 06 * * * /bin/taskrunner "rsnapshot daily" /sbin/rsnapshot -c /etc/rsnapshot.conf daily

# backup weekly (monday) - 6:30
30 06 * * 1 /bin/taskrunner "rsnapshot weekly" /sbin/rsnapshot -c /etc/rsnapshot.conf weekly

# backup monthly (5th) - 6:10
10 06 5 * 0 /bin/taskrunner "rsnapshot monthly" /sbin/rsnapshot -c /etc/rsnapshot.conf monthly
```

## Configuration ##

Each host require its own api key set via `/etc/taskrunner.conf`. This file also contains the API endpoint url.

File: **/etc/taskrunner.conf**

```bash
# logging endpoint url
API_URL="https://tasks.example.org/log"

# api key/token to identify the source
API_KEY="xVibkYrOAYKQFrFbhsqJ"
```

## HTTP Post Params ##

The following variables are send via POST request:

* `title` - the task-name passed as first argument
* `status` - the return/exit code of the command passed as second argument
* `content` - stdout/stderr of the executed command
* `t0` - execution start time of the process - unix timestamp
* `t1` - execution stop time of the process - unix timestamp

### Authentication ###

The APIKEY (token/bearer authentication) is send via the http header field `X-APIKEY` as plaintext.

**TLS/SSL transport encryption is strongly recommended**

## Contribution ##

The **.deb** package is automatically generated via a **Continuous Delivery Pipeline** - please do not build packages manually!

## License ##
taskrunner-sh is OpenSource and licensed under the Terms of [Mozilla Public License 2.0](https://opensource.org/licenses/MPL-2.0). You're welcome to [contribute](docs/CONTRIBUTING.md)
