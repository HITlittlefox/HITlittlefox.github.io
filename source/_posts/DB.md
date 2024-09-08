---
title: DB
category: Backend
date: 2024-08-31 15:25:32
tags: DB
---

# ORMs And ACID

1. [ORMs](https://stackoverflow.com/questions/1279613/what-is-an-orm-how-does-it-work-and-how-should-i-use-one)
2. ACID
    1. Atomicity: the “all or nothing” rule — the transaction either happens completely or doesn’t happen at all
    2. Consistency: data is consistent before and after a transaction without any missing steps
    3. Isolation: multiple transactions can happen concurrently without reading the wrong data
    4. Durability: transactional success is robust to system failure
3. [Transactions](https://fauna.com/blog/database-transaction)
    1. rollback
    2. commit
4. N+1 查询：运行一个查询来获取类别列表，然后运行另一个查询来获取每 N 个类别