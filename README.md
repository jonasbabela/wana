# Wana – Web Log Analyzer (Shell Script)

## Overview

Wana is a shell script tool for analyzing web server log files. It filters log entries and generates basic statistics such as IP lists, URI lists, hostnames, and histograms of requests over IPs or time.

The tool supports working with plain text logs as well as gzip-compressed files.

## Features

* Filtering log entries by:

  * time range (`-a`, `-b`)
  * source IP (`-ip`)
  * URI (`-uri`, regex support)
* Extracting unique values:

  * source IP addresses
  * hostnames (resolved via `host`)
  * requested URIs
* Generating histograms:

  * request count per IP (`hist-ip`)
  * request load per hour (`hist-load`)
* Works with multiple log files or standard input
* Supports `.gz` compressed logs

## Usage

```bash id="q1p8l2"
wana [FILTER] [COMMAND] [LOG [LOG2 [...]]]
```

If no command or filter is provided, raw log data is printed.

## Commands

* `list-ip` – list unique source IPs
* `list-hosts` – list resolved hostnames
* `list-uri` – list requested URIs
* `hist-ip` – histogram of requests per IP (sorted by frequency)
* `hist-load` – hourly request load histogram

## Filters

* `-a DATETIME` – after (exclusive)
* `-b DATETIME` – before (exclusive)
* `-ip IP` – filter by source IP (IPv4/IPv6)
* `-uri REGEX` – filter by URI pattern

Datetime format:

```
YYYY-MM-DD HH:MM:SS
```

## Output format

### Lists

* One item per line
* Unique values only
* Order is not guaranteed (unless specified by command)

### Histograms

Format:

```
CATEGORY (COUNT): #####
```

* `hist-ip` sorted by frequency (descending)
* `hist-load` grouped by hour (`YYYY-MM-DD HH:00`)

## Requirements

* POSIX-compatible shell (bash/dash/ksh)
* GNU tools allowed (`awk`, `sed`, etc.)
* No Python / Perl / Ruby
* No temporary files
* No modification of input files

## Implementation notes

* Uses `host` for reverse DNS lookup
* Supports IPv4 and IPv6 (treated as strings)
* Works with piped input or file arguments
* Handles `.gz` logs transparently

## Key concepts

* Text processing in shell
* Log parsing
* Filtering pipelines
* Aggregation and counting
* Histogram generation
* Working with system utilities (`awk`, `sed`, `sort`, `uniq`)

## Disclaimer

This project was created as part of a university assignment focused on shell scripting, text processing, and log analysis.
