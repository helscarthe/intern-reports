# Shell Scripts / Bash scripting

### Assignment 1: Comparing numbers

```bash
#! /usr/bin/bash

read x
read y

if [ $x -lt $y ]
then
  echo X is less than Y
elif [ $x -gt $y ]
then
  echo X is greater than Y
elif [ $x -eq $y ]
then
  echo X is equal to Y
fi
```
<img src=images/lab-3/image-1.png width=300>

### Assignment 2: Calculate the math expression

```bash
#! /usr/bin/bash

read expression

res=$(echo "scale=3; $expression" | bc)

echo $res
```
<img src=images/lab-3/image-2.png width=300>

### Assignment 3: Unique number(s)

```bash
#! /usr/bin/bash

read len
read list

echo $list | tr ' ' '\n' | sort | uniq -u
```
<img src=images/lab-3/image-3.png width=300>
