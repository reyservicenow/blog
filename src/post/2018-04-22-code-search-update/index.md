---
title: "Code Search Updated"
subtitle: ""
summary: ""
date: 2018-04-22T20:25:56-05:00
---

After some back and forth between the creator of the `sn_codesearch` app
[Cory Seering](https://community.servicenow.com/community?id=community_user_profile&user=bf225e65dbd81fc09c9ffb651f9619d6)
I have a better understanding of how this works.

This scoped app now uses its own search group to search 49 tables
instead of the default 29.

It now includes everything OOB I can think of that could run code
server/client side.

## Setup

1.  Open Studio on your environment
2.  Import from source
3.  Paste in the following URL:
    <https://github.com/jacebenson/servicenow-code.git>

## Update

For those who already installed it;

1.  Open Studio on your environment
2.  Select `Code Search for SP`
3.  Source Control-Apply Remote Changes

This will make the app much smaller as it also moves the scopes from
before.

## Usage

After you import this you can start to use it by navigating to `/code`
on your instance.
