# Clash Tracing Dashboard

An example of a clash tracing exporter API ported for WINDOWS

### Screenshot

![screenshot](https://s2.loli.net/2024/03/02/TSkzsKPm21bpVf8.png)


### How to use

1. ~~modify `.env` and start (`docker-compose up -d`)~~ Modify `docker-compose.yml`

   Modifying `.env`  in windows somehow seems to be of no effect as it does not perform the inline replacement to the docker-compose file.
   So I directly apply the changes to the docker-compose.yml file under the main directory
   To make it work on your machine, one should first look for the `external-controller` address of clash core which is dictated in `C:/<Users>/<username>/.config/clash/config.yaml` (for linux user it should be `/home/.config/clash/config.yaml`. Look for the port number of this field, then replace your controller's port number with that in docker-compose.yml. Specifically, replace the port number after variable `host.docker.internal` in line 35 and line 42 (the variable `host.docker.internal` is used for compativeness on Windows).

2. Enable `tracing` for clash core and run `docker-compose up -d` in this directory

3. Go to `localhost:13000` and login to Grafana, look for the `clash` card in `dashboard` section.

4. Done if data shows up.

### Debug

You should see if the containers are properly raised by the docker. If data aren't received, check the logs in each container. Especially, if no `info` log comes up  in `loki` container, your clash might not presenting any log records. If error logs appear in `traffic*` containers, you are having communication trouble with the clash export ports. Try checking line 35 and line 42 of `docker-compose.yml` along with the error log in these containers. You can also use websocket toolkit to examine if your external-controller address is correct.

> Linux users are theoretically able to follow the config in this repo, but I haven't done testing on platform other than Windows
