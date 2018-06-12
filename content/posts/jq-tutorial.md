---
title: jq tutorial
date: 2016-06-24 16:48:39
tags:
    - jq
---
Example json file
```json
{
  "id": {
    "bioguide": "E000295",
    "thomas": "02283",
    "fec": [
      "S4IA00129"
    ],
    "govtrack": 412667,
    "opensecrets": "N00035483",
    "lis": "S376"
  },
  "name": {
    "first": "Joni",
    "last": "Ernst",
    "official_full": "Joni Ernst"
  },
  "bio": {
    "gender": "F",
    "birthday": "1970-07-01"
  },
  "terms": [
    {
      "type": "sen",
      "start": "2015-01-06",
      "end": "2021-01-03",
      "state": "IA",
      "class": 2,
      "state_rank": "junior",
      "party": "Republican",
      "url": "http://www.ernst.senate.gov",
      "address": "825 B&C Hart Senate Office Building Washington DC 20510",
      "office": "825 B&c Hart Senate Office Building",
      "phone": "202-224-3254"
    }
  ]
}
```


+ query a attribute
```bash
$ jq '.name' example.json
{
  "first": "Joni",
  "last": "Ernst",
  "official_full": "Joni Ernst"
}
```
+ query nested attribute
```bash
$ jq '.name.first' example.json
"Joni"
```

+ query a array
```bash
$ jq '.terms[0]' example.json
{
  "type": "sen",
  "start": "2015-01-06",
  "end": "2021-01-03",
  "state": "IA",
  "class": 2,
  "state_rank": "junior",
  "party": "Republican",
  "url": "http://www.ernst.senate.gov",
  "address": "825 B&C Hart Senate Office Building Washington DC 20510",
  "office": "825 B&c Hart Senate Office Building",
  "phone": "202-224-3254"
}
```

+ select(boolean_expression)

`select(x)` produces its input unchanged if `x` returns true for that input, and produces no output otherwise.

```bash
$ jq '.terms[] | select(.class == 2)' example.json
{
  "type": "sen",
  "start": "2015-01-06",
  "end": "2021-01-03",
  "state": "IA",
  "class": 2,
  "state_rank": "junior",
  "party": "Republican",
  "url": "http://www.ernst.senate.gov",
  "address": "825 B&C Hart Senate Office Building Washington DC 20510",
  "office": "825 B&c Hart Senate Office Building",
  "phone": "202-224-3254"
}
```
**Notice: particular attribute such as numbers should use quotes**
+ to_entries, from_entries, with_entries

These functions convert between an object and an array of key-value pairs. If to_entries is passed an object, then for each k: v entry in the input, the output array includes {"key": k, "value": v}.

from_entries does the opposite conversion, and with_entries(foo) is a shorthand for to_entries | map(foo) | from_entries, useful for doing some operation to all keys and values of an object. from_entries accepts key, Key, name, Name, value and Value as keys.

```
jq 'to_entries'
Input	{"a": 1, "b": 2}
Output	[{"key":"a", "value":1}, {"key":"b", "value":2}]

jq 'from_entries'
Input	[{"key":"a", "value":1}, {"key":"b", "value":2}]
Output	{"a": 1, "b": 2}

jq 'with_entries(.key |= "KEY_" + .)'
Input	{"a": 1, "b": 2}
Output	{"KEY_a": 1, "KEY_b": 2}
```
+ change field value

```
jq '.name="1"|.resource="2"'
Input {"name":"a","resource":"b"}
Ouput {"name":"1","resource":"b"}
```
+ show select fields

```
jq '.name,.resource'
Input {"name":"a","resource":"b","type":"c"}
Output "a" "b"
```