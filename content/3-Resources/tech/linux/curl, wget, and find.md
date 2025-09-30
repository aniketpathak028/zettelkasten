---
title: curl, wget and find
draft: false
tags:
  - curl
  - wget
  - find
date: 2025-09-24
description: fetching and searching
---
# curl, wget and find

### curl

- stands for Client URL
- fetches stuff from the internet using protocols like HTTP, HTTPS, FTP and more
- can be used for REST APIs, download / upload files, send form data and debug n/w requests
```bash
curl [option] [URL]
```

> Use curl when you want to **fetch, send, test, or debug network requests** directly from the shell. It’s like your Swiss‑army knife for HTTP and APIs

```bash
# fetch html of a webpage
curl http://example.com

# send form data
curl -X POST -d "username=alice&password=1234" http://example.com/login

# file upload
curl -F "file=@report.pdf" http://example.com/upload
```
### wget

- stands for web get
- used for downloading files from the web
- supports http, https, and ftp
- unlike curl, which can do all sorts of data transfers, wget is specialized for downloading files!

```bash
wget [options] [URL]
```

> use wget when you want to download files or mirror websites.
> use curl when you want to interact with data and APIs.

```bash
# download a file
wget http://example.com/file.zip

# save with a diff name
wget -O myfile.zip http://example.com/file.zip

# resume a broken download
wget -c http://example.com/bigfile.iso

# download multiple files
wget -i filelist.txt
```
### find

find files or dir in the system
```bash
find [path] [options] [expression] [action]
```

- **path** → Where to start searching (e.g., /, ., /home/user)
- **options/expression** → Criteria like name, size, user, type, etc.
- **action** → What to do with the results (print, delete, exec another command, etc.)

If you don’t provide a path, find defaults to the **current directory (.)**.

ex-
```bash
# find by name
find /home -name "file.txt"

# find by type "files" only
find . -type f -name "report*"

# find by size
find . -type f -size +50M
```

## Links:

[[linux]]
[[shell]]

202509241745