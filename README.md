# Logjammin'

A batch time logger for JIRA

## Prerequisites:

- Python 3 is required.
- The [`pytz`](https://pypi.python.org/pypi/pytz) and [`jira`](https://pypi.python.org/pypi/jira) Python packages must be installed.
- A JSON configuration file must exist at the path `~/.logjammin`. The file has the following format:
```json
{
    "host": "your JIRA hostname",
    "user": "your JIRA username",
    "password": "your JIRA password",
    "time_zone": "your tzdata time zone ID (e.g. US/Pacific)"
}
```
- An optional `log_file` property can be set instead of specifying the log file via a command line argument.

## Usage:

```
$ ./logjammin.py -h
usage: logjammin.py [-h] [-p] [file]

positional arguments:
  file              the file to load

optional arguments:
  -h, --help        show this help message and exit
  -p, --parse-only  parse the file only (don't verify tickets or upload logs)
```

As the file is parsed, each ticket is fetched from JIRA to ensure it exists. After parsing, a summary of the logs is presented for review along with a prompt to indicate whether or not to upload the logs to JIRA.

## Time Log File Format:

The general format of the time log file is as follows:

```
YYYY-MM-DD
TICKET-123, 90m
TICKET-456, 1h 30m, added new feature

YYYY-MM-DD
TICKET-789, 1.5h
```

- Dashes in date strings are optional.
- Blank lines are allowed but not required.
- Whitespace is allowed but not required, e.g. `TICKET-123,1h30m` and `TICKET-456 , 1 h 30 m` are both valid log entries.
- Ticket IDs and time entries are case-insensitive.
- Dates can be repeated.
