# redis-cli-comamnd-
redis-cli comamnd 


## A: install redis

windows
```
https://github.com/microsoftarchive/redis/releases
run 2 file redis-server and redis-cli (add folder to path)
```
ubuntu
```
sudo apt update
sudo apt install redis-server

ufw allow 6379
ufw allow 6379/tcp

sudo systemctl status redis
```

## B: Commond command
init redis server
```
redis-server
```
init redis server

```
redis-cli
```

### 1.String
#### get and set name
```
set name "nghia hsgs"
get name
```

#### list all keys
```
keys *
keys name*
```

#### delete value of one key, => nil
```
del key_name
keys * => disappaear key_name
```

#### delete all data (every thing in redis)
```
flushall
```

#### set name with expire time
```
timeout 10s
setex name 10 "nghia"
timeout 10ms
psetex name 10 "nghia"
```

#### check time to live
```
ttl name
```

#### if set normal, ttl = -1
```
set name "nghiahsgs"
ttl name
```

#### set key if key exits => ignore (preserve old value)
```
set name "trang"
setnx name "nghia" => 0
get name => trang
```

#### if name2 does't exits => create new key
```
setnx name2 "nghiadz"
get name2
```

#### check length of string
```
set name "trang"
strlen name
```

#### multi set value
```
mset name1 "nghia" name2 "trang"
that means :
name1 => "nghia"
name2 => "trang"
```

#### increase and decrease number
```
set num 10
incr num
get num

set num 10
decr num
get num
```

#### increase by and decrease by
```
incrby num 5
decrby num 5
```

#### append to string
```
set name "nghia"
append name " hsgs"
get name => "nghia hsgs"
```


### 2.Pubsub
```
subscribe channel_nghia
publish channel_nghia "abc"

psubscribe channel*
publish channel_nghia "abc"
```
### 3.Hash
giống kiểu object trong js
```json
{
  "user1":{
    "name":"nghia",
    "age":20
  },
  "user2":{
    "name":"nghia2",
    "age":25
  }
}
```

#### hmset
```
vd khi muốn lưu 
student1 có name nghia, age 20, class 11A1
student2 có name nghia2, age 21, class 12A1

hmset student1 name "nghia" age 20 class 11A1
hmset student2 name "nghia2" age 21 class 12A1
```

#### hget: get value of one fields of obj
```
hget student1 name => nghia
hget student2 name => nghia2
```

#### hgetall : get all key and value of one obj
```
hgetall student1
```

#### hexists: check one field is exists or not
```
hexists student1 name
```

#### hdel: delete one field of obj (hash)
```
hdel student1 name
```

#### hsetnx: set value for one field, if field exists
```
hsetnx student1 name "nghiadz"
```

#### hkeys:get all fields
```
hkeys user1
```

#### hvals: get all values of all fields
```
hvals user1
```

#### inscrease by and decease by value
```
hmset user1 name "nghia" age 20
hincrby user age 20
hget user1 age
```

#### hlen: return number fields of hash
```
hlen user1
```

#### hmget get multiple value of field of hash
```
hmget user1 name age
```

### 4.List

#### monitor all statement excuted
redis-cli monitor

#### lpush value to list
```
lpush L 1 2 3
lrange L start stop
lpush L 4
lpop L

rpush L 1 2 3 4
rpop L
```

#### get length of list
```
llen L
```

#### get value of index in list
```
lindex L 1
```
#### assign value for list
```
lset L 0 100
lset L 100 200 => ERR index out of range
```
#### loop all value of list
```
lrange L 0 -1
```

#### if list exits => push
```
lpushx L 10
rpushx L 10
```

#### insert value to list
```
linsert L before _value new_element
lrange L 0 -1
```

### 5.SET
(set : collections of unique values)


#### add number to set
```
sadd s1 1 2 3 4
```

#### list all member of set
```
smembers s1
```

#### length of a set
```
scard s1
```

#### get diff
```
sadd s1 1 2 3
sadd s2 2 3 4
sdiff s1 s2 => 1
sdiff s2 s1 => 4
```

#### get diff and store new set
```
sadd s1 1 2 3
sadd s2 2 3 4
sdiffstore s3 s1 s2
smembers s3 => 1
```

#### get union of 2 set
```
sunion s1 s2
sunionstore s3 s1 s2
```

#### remove element in set
```
srem s1 1 2
```

#### remove random element in set
```
spop s1 nb_remove
```

#### get intersection of 2 set
```
sadd s1 1 2 3
sadd s2 2 3 4
sinter s1 s2
sinterstore s3 s1 s2
```

#### move element from set a to set b
```
smove set_from set_dest value
smove s2 s1 30
```

### ORDERED SET
