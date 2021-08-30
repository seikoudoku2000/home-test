# home-test

## Requirement
- Docker
  - tested only with version 20.10.8, but it would work in recent versions


## HOW TO RUN
```
# Build a docker image
$ cd home-test
$ docker build --tag home-test .

# Run
## Please change URLs and --metadata parameter according to your necessity
$ docker run --rm -v $(pwd)/output:/app/output home-test https://qiita.com/ https://qiita.com/seikoudoku2000 https://seikoudoku2000.com https://autify.com --metadata
fetching: https://qiita.com/...
saved result: output/qiita.com/ROOT/20210830004051.html
saved result: output/qiita.com/ROOT/20210830004051.metadata
fetching: https://qiita.com/seikoudoku2000...
saved result: output/qiita.com/seikoudoku2000/20210830004051.html
saved result: output/qiita.com/seikoudoku2000/20210830004051.metadata
fetching: https://seikoudoku2000.com...
Failed fetching: https://seikoudoku2000.com
HTTPSConnectionPool(host='seikoudoku2000.com', port=443): Max retries exceeded with url: / (Caused by NewConnectionError('<urllib3.connection.HTTPSConnection object at 0x7f61c200b4c0>: Failed to establish a new connection: [Errno -2] Name or service not known'))
fetching: https://autify.com...
saved result: output/autify.com/ROOT/20210830004051.html
saved result: output/autify.com/ROOT/20210830004051.metadata

# Result
## Result files are saved under "output" directory. 
## And files named yyyyMMddHHmmss.html and yyyyMMddHHmmss.metadata are created  
## They're not configurable in the current implementation (PR is welcomed!!)
 
$ tree output/
output/
├── autify.com
│ └── ROOT
│     ├── 20210830004051.html
│     └── 20210830004051.metadata
└── qiita.com
    ├── ROOT
    │ ├── 20210830004051.html
    │ └── 20210830004051.metadata
    └── seikoudoku2000
        ├── 20210830004051.html
        └── 20210830004051.metadata
```


## Usage
```
$ docker run --rm home-test -h
usage: fetch [-h] [--metadata] URSs [URSs ...]

Fetch and save web pages

positional arguments:
  URSs        Urls to fetch and save the page

optional arguments:
  -h, --help  show this help message and exit
  --metadata  Save metadata as well (number of links, number of images and
              fetch date)
```

## Future TODOs
- Test code, CI/CD
- Proper error handling 
  - Change behavior according to kind of error
  - In some cases, it would be nice to save error stacktrace itself for later investigation 
- Deal with URL parameters
- Make output directory and file name configurable
- Make command execution more intuitive using some wrapper tool (e.g. Makefile, [variant](https://github.com/mumoshu/variant))