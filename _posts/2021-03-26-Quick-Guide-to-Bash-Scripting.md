---
layout: post
title:  "Quick Guide to Bash Scripting"
date:   2020-11-20 09:30:00 +0000
tags:   bash, arrays, safe, scripting
p_tags: note
meta:
    keywords: "cheatsheet, bash, scripting, arrays, safe"
---

<p align="center">
<img src="/assets/images/bash_googling.png"  title="Googling Bash"/>
</p>

Making a script safe

```bash
# Enables exiting of a script on failure of a command, even if it's part of a pipe command (with good output)
set -Eeo pipefail
```

Writing functions

```bash
# function writing to the stderr
function log_info() {
    >&2 echo "INFO: ${*}"
}

# function call to log stuff
log_info "Finished executing the script and changes have been pushed with all the success! :)"
```

Returning a variable with `echo`

```bash
# function declaring local variable, doing some stuff and returning 
function list_a_few_things_from_file() {
    local few_things
    
    few_things=$(cat my_file) # my file has things separated by a newline
    echo $few_things | sort | uniq
}

# calling our function
unique_sorted_things=$(list_a_few_things_from_an_api)
for thing in $unique_sorted_things; do
    log_info "Well, this is the thing: $thing"
done
```