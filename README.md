##About
This project uses sqlite3 libcurl and uses the [acd_cli](https://github.com/yadayada/acd_cli/) sqlite db.
This idea is to accelerate the acd_cli fuse mount using some c.

##TODO
- ~~set st_ctime and st_mtime in SQLcallback_getattr~~ 
- handle database locked
- seems to have issues on armhf.
- also has issues with relative paths (might be libfuse)

##build
``` gcc acdfuse.c `pkg-config fuse sqlite3 libcurl --cflags --libs` -ggdb -o acdfuse; ```

##mount
./acdfuse [-d]  mountpoint [-o options]

##Benchmark

### acdfuse_c
```
./acdfuse acd/
time find acd/ > /dev/null

real	0m10.172s
user	0m0.060s
sys	0m0.193s
```

###acd_cli
```
acd_cli mount acd/
time find acd/ > /dev/null

real	4m25.864s
user	0m0.233s
sys	0m0.703s
```
