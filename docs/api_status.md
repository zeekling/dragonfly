The following document describes the current API status
with respect to Memcached and Redis APIs.

## Memcache API
- [X] set
- [X] get
- [X] replace
- [X] add
- [X] stats (partial)
- [x] append
- [x] prepend
- [x] delete
- [x] flush_all
- [x] incr
- [x] decr
- [x] version
- [x] quit


## Redis API

### API 1
- [X] String family
  - [X] SET
  - [X] SETNX
  - [X] GET
  - [X] DECR
  - [X] INCR
  - [X] DECRBY
  - [X] GETSET
  - [X] INCRBY
  - [X] MGET
  - [X] MSET
  - [X] MSETNX
  - [X] SUBSTR
- [x] Generic family
  - [X] DEL
  - [X] ECHO
  - [X] EXISTS
  - [X] EXPIRE
  - [X] EXPIREAT
  - [X] KEYS
  - [X] MOVE
  - [X] PING
  - [X] RENAME
  - [X] RENAMENX
  - [X] SELECT
  - [X] TTL
  - [X] TYPE
  - [X] SORT
- [X] Server Family
  - [X] AUTH
  - [X] QUIT
  - [X] DBSIZE
  - [ ] BGSAVE
  - [X] SAVE
  - [X] DEBUG
  - [X] EXEC
  - [X] FLUSHALL
  - [X] FLUSHDB
  - [X] HELLO
  - [X] INFO
  - [X] MULTI
  - [X] SHUTDOWN
  - [X] LASTSAVE
  - [X] SLAVEOF/REPLICAOF
  - [ ] SYNC
- [X] Set Family
  - [x] SADD
  - [x] SCARD
  - [X] SDIFF
  - [X] SDIFFSTORE
  - [X] SINTER
  - [X] SINTERSTORE
  - [X] SISMEMBER
  - [X] SMOVE
  - [X] SPOP
  - [ ] SRANDMEMBER
  - [X] SREM
  - [X] SMEMBERS
  - [X] SUNION
  - [X] SUNIONSTORE
- [X] List Family
  - [X] LINDEX
  - [X] LLEN
  - [X] LPOP
  - [X] LPUSH
  - [X] LRANGE
  - [X] LREM
  - [X] LSET
  - [X] LTRIM
  - [X] RPOP
  - [X] RPOPLPUSH
  - [X] RPUSH
- [X] SortedSet Family
  - [X] ZADD
  - [X] ZCARD
  - [X] ZINCRBY
  - [X] ZRANGE
  - [X] ZRANGEBYSCORE
  - [X] ZREM
  - [X] ZREMRANGEBYSCORE
  - [X] ZREVRANGE
  - [X] ZSCORE
- [ ] Other
  - [ ] BGREWRITEAOF
  - [x] MONITOR
  - [ ] RANDOMKEY

### API 2
- [X] List Family
  - [X] BLPOP
  - [X] BRPOP
  - [ ] BRPOPLPUSH
  - [X] LINSERT
  - [X] LPUSHX
  - [X] RPUSHX
- [X] String Family
  - [X] SETEX
  - [X] APPEND
  - [X] PREPEND (dragonfly specific)
  - [x] BITCOUNT
  - [ ] BITFIELD
  - [x] BITOP
  - [x] BITPOS
  - [x] GETBIT
  - [X] GETRANGE
  - [X] INCRBYFLOAT
  - [X] PSETEX
  - [x] SETBIT
  - [X] SETRANGE
  - [X] STRLEN
- [X] HashSet Family
  - [X] HSET
  - [X] HMSET
  - [X] HDEL
  - [X] HEXISTS
  - [X] HGET
  - [X] HMGET
  - [X] HLEN
  - [X] HINCRBY
  - [X] HINCRBYFLOAT
  - [X] HGETALL
  - [X] HKEYS
  - [X] HSETNX
  - [X] HVALS
  - [X] HSCAN
- [X] PubSub family
  - [X] PUBLISH
  - [X] PUBSUB
  - [X] PUBSUB CHANNELS
  - [X] SUBSCRIBE
  - [X] UNSUBSCRIBE
  - [X] PSUBSCRIBE
  - [X] PUNSUBSCRIBE
- [X] Server Family
  - [X] WATCH
  - [X] UNWATCH
  - [X] DISCARD
  - [X] CLIENT LIST/SETNAME
  - [ ] CLIENT KILL/UNPAUSE/PAUSE/GETNAME/REPLY/TRACKINGINFO
  - [X] COMMAND
  - [X] COMMAND COUNT
  - [ ] COMMAND GETKEYS/INFO
  - [ ] CONFIG GET/REWRITE/SET/RESETSTAT
  - [ ] MIGRATE
  - [ ] ROLE
  - [ ] SLOWLOG
  - [ ] PSYNC
  - [ ] TIME
  - [ ] LATENCY...
- [X] Generic Family
  - [X] SCAN
  - [X] PEXPIREAT
  - [ ] PEXPIRE
  - [x] DUMP
  - [X] EVAL
  - [X] EVALSHA
  - [ ] OBJECT
  - [x] PERSIST
  - [X] PTTL
  - [x] RESTORE
  - [X] SCRIPT LOAD/EXISTS
  - [ ] SCRIPT DEBUG/KILL/FLUSH
- [X] Set Family
  - [X] SSCAN
- [X] Sorted Set Family
  - [X] ZCOUNT
  - [X] ZINTERSTORE
  - [X] ZLEXCOUNT
  - [X] ZRANGEBYLEX
  - [X] ZRANK
  - [X] ZREMRANGEBYLEX
  - [X] ZREMRANGEBYRANK
  - [X] ZREVRANGEBYSCORE
  - [X] ZREVRANK
  - [X] ZUNIONSTORE
  - [X] ZSCAN
- [ ] HYPERLOGLOG Family
  - [ ] PFADD
  - [ ] PFCOUNT
  - [ ] PFMERGE

### API 3
- [X] Generic Family
  - [X] TOUCH
- [X] HashSet Family
  - [X] HSTRLEN
- [X] Server Family
  - [ ] CLIENT REPLY
  - [X] REPLCONF
  - [ ] WAIT

### API 4
- [X] Generic Family
  - [X] UNLINK
- [ ] Server Family
  - [ ] MEMORY USAGE/STATS/PURGE/DOCTOR
  - [ ] SWAPDB

### API 5
- [X] Stream Family
  - [X] XADD
  - [ ] XCLAIM
  - [X] XDEL
  - [X] XGROUP CREATE/DELCONSUMER/DESTROY/HELP/SETID
  - [ ] XGROUP CREATECONSUMER
  - [X] XINFO GROUPS/HELP
  - [ ] XINFO CONSUMERS/GROUPS/STREAM
  - [X] XLEN
  - [ ] XPENDING
  - [X] XRANGE
  - [ ] XREAD
  - [ ] XREADGROUP
  - [X] XREVRANGE
  - [X] XSETID
  - [ ] XTRIM

- [X] Sorted Set Family
  - [X] ZPOPMIN
  - [X] ZPOPMAX

### API 6
- [X] String Family
  - [X] GETEX

- [X] Set Family
  - [X] SMISMEMBER

- [X] List Family
  - [X] LMOVE
  - [X] LPOS

- [ ] Stream Family
  - [ ] XAUTOCLAIM

- [ ] Sorted Set Family
  - [ ] ZUNION

## Notes
Some commands were implemented as decorators along the way:

 - [X] ROLE (2.8) decorator as master.
 - [X] BGSAVE (decorator for save)
 - [X] FUNCTION FLUSH (does nothing)
