# home-test

## HOW TO RUN
```
# build a docker image
$ docker build --tag home-test .

# run
$ docker run --rm -v $(pwd)/output:/app/output home-test https://qiita.com/seikoudoku2000 --metadata
```