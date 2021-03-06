# What's this?
- Launch [WebPagetest](https://github.com/WPO-Foundation/webpagetest) by Docker

# Why do you re-build docker images?
- Because the containers created by raw images return incorrect results (can't get results)
    - Detail is below, the article at `Reference`

# Procedure
- Build docker images
    - server
    - agent
- Run docker containers
    - server
    - agent
- Access to WebPagetest!
    - http://localhost:4000/

# All tasks in one shell script
- If containers remain, `docker run` will fail so you must remove containers.

```bash
$ ./build_and_run.sh
```

# Build docker images only
```bash
$ docker build -t local-wptserver ./server
$ docker build -t local-wptagent ./agent
```

# Run docker containers only
```bash
$ docker run -d -p 4000:80 --name local-wptserver local-wptserver
$ docker run -d -p 4001:80 --name local-wptagent --network="host" -e "SERVER_URL=http://localhost:4000/work/" -e "LOCATION=Test" local-wptagent
```

# Reference
- [Local WebPagetest Using Docker – Francis John – Medium](https://medium.com/@francis.john/local-webpagetest-using-docker-90441d7c2513)

# LICENSE
- [MIT License](LICENSE)
