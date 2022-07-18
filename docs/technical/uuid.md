# [UUIDs explained](https://www.sohamkamani.com/uuid-versions-explained/)

TLDR
- use v4 unless there's specific scenarios

## UUID v1
- MAC address + current datetime
    - `71226380-06c0-11ed-8d75-e9e11a03a4b7`
- UUID v1 generated a few seconds later
    - `7c2e73e0-06c0-11ed-8d75-e9e11a03a4b7`
- guarantee that there's random

## UUID v4

- random numbers
- unlikely there's a conflict (2^128)

## UUID v5

UUIDv5(namespace_uuid, text)
![uuidv5.png](uuidv5.png)

avoiding rainbow table attacks by using UUIDv5 as a salt for passwords