---
title: powers of shell scripting
draft: false
tags:
  - shell-scripting
  - bash
  - linux
  - automation
date: 2025-09-25
description: powers of shell scripting!
---
# powers of shell scripting 🔥

I had always underestimated the power of shell scripting, assuming programming languages like python, go are much more powerful , however I have come to realization why any high level programming language can't come close to shell scripts because of the following reasons:

- shell commands are native to kernels and thus are extremely fast, portable and compatible unlike programming languages which need a proper setup
- although writing a script in python may be easier, the flexibility that a shell script provides is unmatched when it comes to dealing with kernel level resources like processes, memory and networking stuff!
- lastly shell scripts are cool 🆒 one can never understand the unix philosophy of "doing one thing but doing it best way possible!" without using a shell like bash

I recently came across a usecase and thought of sharing the same.

Problem Statement:

there is a folder in my system called dsa, containing a bunch of ipynb files of various data structure and algorithms topics like Trees, Graphs, Dynamic Programming etc

I wanted to host these files online in my [zettelkasten](https://zet.aniketpathak.me/) so that I could view them anytime and revise the concepts

since my zettelkasten is based on my obsidian vault which is locally just a folder containing a bunch of md files which get rendered as a static site, all I needed to do was to convert these ipynb files into md files in a specific location inside my obsidian vault.

simple!? ehhh 

yes, but there was one catch this should be done only when there was a change in the file, so if there are 10 files, and only 2 files have changed since the last time I ran the script, it should not convert all the 10 files and override, instead it should only convert these 2 files.


here is the script that i came up with, and it works like a charm

```bash
# !/bin/bash

# variables
SRC_DIR="/Users/aniket/workspace/dsa"
DEST_DIR="/Users/aniket/REPOS/zet/content/3-Resources/tech ⚙️/dsa 🧠"
STATE_FILE="$HOME/.deployDsa"

# check if the dir exists
mkdir -p "$DEST_DIR"

# read last run timestamp
if [[ ! -f "$STATE_FILE" ]]; then
  echo "ℹ️No last run record found -> converting all notebooks..."
  last_run=0
else
  last_run=$(cat "$STATE_FILE")
fi

# current time
now=$(date +%s)

# loop through all the ipynb files in source and check if newer than last run
for notebook in "$SRC_DIR"/*.ipynb; do
  base=$(basename "$notebook")
  # notebook modification time
  modTime=$(stat -f "%m" "$notebook") # macOs
  # modTime=$(stat -c "%Y" "$notebook") # linux

  if ((modTime > last_run)); then 
    if jupyter nbconvert --to markdown --embed-images "$notebook" --output-dir "$DEST_DIR" >/dev/null 2>&1; then
        echo "✅ converted $base"
    else
        echo "❌ failed to convert $base"
    fi
  else
    echo "Skipping (no change): $notebook"
  fi
done

# update the last run timestamp
echo "$now" > "$STATE_FILE"

echo "✅ Conversion complete for updated notebooks."

```
### working of the script

- the script first checks if the destination folder exists or not and incase it doesn't exists, creates one
- then it loops through all the ipynb files in the source folder and maintains a time stamp file which maintains the time when the script ran last time
- incase the file is modified after the script ran last time, it converts the file otherwise it doesn't 🦸
- once the conversion is complete, it changes the time stamp to the current time

and that's how the shell script saves lives of struggling developers!
## Links:

[[shell]]
[[linux]]

202509251953