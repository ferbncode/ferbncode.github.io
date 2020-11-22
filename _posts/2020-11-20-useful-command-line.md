---
layout: post
title:  "jq, awk, vim, xargs! :)"
date:   2020-11-20 09:30:00 +0200
tags: jq, awk, vim, gist, xargs
p_tags: note
meta:
    keywords: "cheatsheet, jq, awk, vim"
---

It's undoubtedly best to open documentation for learning anything. But, it doesn't hurt to write down some code to speed
things for the next time! :) 

This is a public and easy (and running!) cheatsheet/notes for some of the (formatting) commands that I find 
super-useful. Some of them might feel like taking three right turns for a left, but they seem to do what I want to do!

## jq
Find main documentation [here](https://stedolan.github.io/jq/tutorial/).

*Get a field from array!*
```json
[{
    "name": "hello"
    },{
    "name": "world"
}]
```
```bash
cat array.json | jq '.[] | .name'
```
For an array with names, it would be:
```bash
cat array-with-name.json | jq .items[].id'
```


*Filter and list!*
```json
[{
    "name": "hello",
    "comp": 1
    },{
    "name": "world",
    "comp": 3
}]
```
```
cat array.json | jq -c '.[] | select ( .comp <= 2 ) | .name'
```

*Convert a list to json array*

```json
[{
    "name": "hello",
    "comp": 1
    },{
    "name": "world",
    "comp": 3
}]
```
```
cat array.json | jq -c '.[] | select ( .comp <= 2 ) | .name' | jq --slurp
```

*Escaped string > json*
```
"[{\r\n    \"name\": \"hello\",\r\n    \"comp\": 1\r\n    },{\r\n    \"name\": \"world\",\r\n    \"comp\": 3\r\n}]" 
```
```bash
cat array_string.json | jq '. | fromjson'
```
This is particularly useful with reading Kubernetes configmaps with json data
```bash
kubectl get configmap test -n test-namespace -p json | jq '.data["queries.json"] | fromjson | .[] | .id'
```

*Raw output - no quoted string*
```bash
cat array.json | jq -r '.[] | .name'
```

*Array contains!*
```json
[{
    "some_list": [1, 2, 3]
},{
    "some_list": [2, 3]
}]
```
```bash
cat some | jq '.[] | select( .some_list[] | contains(1) )' | jq --slurp
```

*Arguments!!*
```json
{
    "test": {
        "password": "test-password"
    },
    "live": {
        "password": "live-password"
    }
}
```
```bash
jq --arg environ "$environment" '.[$environ]' config.json 
```
 
*Json Key with dots!*
```json
{
    "test": {
        "db.url": "test-url"
    },
    "live": {
        "db.url": "live-url"
    }
}
```
```bash
cat config.json | jq '.live["db.url"]'
```

*Transform data easily*
```json
{
    "events": [{
        "metadata": {
            "occurred_at": "2016-03-15T23:47:15+01:00",
        },
        "subscription_id": "random_id",
        "event_type": "random.et",
        "partition": "0"
    },{
        "metadata": {
            "occurred_at": "2016-03-15T23:47:15+01:00",
        },
        "subscription_id": "random_id_2",
        "event_type": "random.et.2",
        "partition": "1"
    }]
}
```
```bash
cat events \
| jq '.events[] | .metadata.occurred_at + ", " + .subscription_id + ", " + .event_type + "," + .partition'
```
```bash
cat events \
| jq '.events[0] | {occurred: .metadata.occurred_at, name: .event_type}'
```

*pipe functions*<br/>
There are many, but I particularly find length useful sometimes. For the above json
```bash
cat events \
| jq '.events | length'
```

# awk

*Split by a delimiter*
```
1/a
2/b
3/c
```
```bash
cat test_file | awk -F / '{print $1}'
```

*Print specific column*

```bash
➜  test git:(master) ✗ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.178.1   0.0.0.0         UG    600    0        0 wlp3s0
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
172.18.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-bab2fd594fa2
172.22.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-f802cdc82922
172.29.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-fdc6a6612112
172.30.0.0      0.0.0.0         255.255.0.0     U     0      0        0 br-2a3e1932dcc0
192.168.178.0   0.0.0.0         255.255.255.0   U     600    0        0 wlp3s0
```
```bash
route -n | awk '{print $8}'
```

## Formatting within vim

Any command can be called on vim (or extended with vim) text editor for formatting the data within.
Some useful ones are as below
```bash
# Format json in a file (in-place)
:%!jq

# Tab separate using `column` (in-place)
:%!column -t

# Remove all trailing whitespace
:%s/\s\+$//e
```
```bash
# Run all commands on a small selected text in vim! :)
# Select text in visual mode and press ':'. This would automatically print :`<,'> and a command can be run using !<cmd>
:'<,'>!somecmd

# More on visual mode - Select last selection again
gv

# Wrap around current block 
vap
```

## xargs

`xargs` is very useful utility for repeating arguments on a single script/command.
```
# Just echo-ing to avoid cleaning
docker images --all | grep "<none>" | awk '{print $3}' | xargs -I {} echo "docker rmi {}"

# Input to xargs
xargs -I {} curl http://localhost.com/queries/{} < curl http://localhost.com/query_ids | jq -r '.id'
```