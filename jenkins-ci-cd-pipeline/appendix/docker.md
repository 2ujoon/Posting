---
description: 각 명령어의 --help 옵션 출력 내용을 옮겨둠
---

# Docker 명령어 참고

옵션 별 arguments 등 세부적인 내용이 궁금하다면 `man COMMAND` 로 확인

<details>

<summary>docker pull</summary>

* 레지스트리에서 컨테이너를 실행할 이미지를 다운로드 한다.

<!---->

* `docker image pull` 의 축약형



### 시놉시스

`docker pull [OPTIONS] NAME[:TAG|@DIGEST]`



### 옵션

```
-a, --all-tags                Download all tagged images in the repository
    --disable-content-trust   Skip image verification (default true)
    --platform string         Set platform if server is multi-platform capable
-q, --quiet                   Suppress verbose output
```

</details>

<details>

<summary>docker run</summary>

* 이미지를 사용해 새 컨테이너를 생성하고 실행한다.



### 시놉시스

`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`



### 옵션

```
    --add-host list                    Add a custom host-to-IP mapping (host:ip)
    --annotation map                   Add an annotation to the container (passed through to the OCI runtime) (default map[])
-a, --attach list                      Attach to STDIN, STDOUT or STDERR
    --blkio-weight uint16              Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
    --blkio-weight-device list         Block IO weight (relative device weight) (default [])
    --cap-add list                     Add Linux capabilities
    --cap-drop list                    Drop Linux capabilities
    --cgroup-parent string             Optional parent cgroup for the container
    --cgroupns string                  Cgroup namespace to use (host|private)
                                       'host':    Run the container in the Docker host's cgroup namespace
                                       'private': Run the container in its own private cgroup namespace
                                       '':        Use the cgroup namespace as configured by the
                                                  default-cgroupns-mode option on the daemon (default)
    --cidfile string                   Write the container ID to the file
    --cpu-period int                   Limit CPU CFS (Completely Fair Scheduler) period
    --cpu-quota int                    Limit CPU CFS (Completely Fair Scheduler) quota
    --cpu-rt-period int                Limit CPU real-time period in microseconds
    --cpu-rt-runtime int               Limit CPU real-time runtime in microseconds
-c, --cpu-shares int                   CPU shares (relative weight)
    --cpus decimal                     Number of CPUs
    --cpuset-cpus string               CPUs in which to allow execution (0-3, 0,1)
    --cpuset-mems string               MEMs in which to allow execution (0-3, 0,1)
-d, --detach                           Run container in background and print container ID
    --detach-keys string               Override the key sequence for detaching a container
    --device list                      Add a host device to the container
    --device-cgroup-rule list          Add a rule to the cgroup allowed devices list
    --device-read-bps list             Limit read rate (bytes per second) from a device (default [])
    --device-read-iops list            Limit read rate (IO per second) from a device (default [])
    --device-write-bps list            Limit write rate (bytes per second) to a device (default [])
    --device-write-iops list           Limit write rate (IO per second) to a device (default [])
    --disable-content-trust            Skip image verification (default true)
    --dns list                         Set custom DNS servers
    --dns-option list                  Set DNS options
    --dns-search list                  Set custom DNS search domains
    --domainname string                Container NIS domain name
    --entrypoint string                Overwrite the default ENTRYPOINT of the image
-e, --env list                         Set environment variables
    --env-file list                    Read in a file of environment variables
    --expose list                      Expose a port or a range of ports
    --gpus gpu-request                 GPU devices to add to the container ('all' to pass all GPUs)
    --group-add list                   Add additional groups to join
    --health-cmd string                Command to run to check health
    --health-interval duration         Time between running the check (ms|s|m|h) (default 0s)
    --health-retries int               Consecutive failures needed to report unhealthy
    --health-start-interval duration   Time between running the check during the start period (ms|s|m|h) (default 0s)
    --health-start-period duration     Start period for the container to initialize before starting health-retries countdown (ms|s|m|h) (default 0s)
    --health-timeout duration          Maximum time to allow one check to run (ms|s|m|h) (default 0s)
    --help                             Print usage
-h, --hostname string                  Container host name
    --init                             Run an init inside the container that forwards signals and reaps processes
-i, --interactive                      Keep STDIN open even if not attached
    --ip string                        IPv4 address (e.g., 172.30.100.104)
    --ip6 string                       IPv6 address (e.g., 2001:db8::33)
    --ipc string                       IPC mode to use
    --isolation string                 Container isolation technology
    --kernel-memory bytes              Kernel memory limit
-l, --label list                       Set meta data on a container
    --label-file list                  Read in a line delimited file of labels
    --link list                        Add link to another container
    --link-local-ip list               Container IPv4/IPv6 link-local addresses
    --log-driver string                Logging driver for the container
    --log-opt list                     Log driver options
    --mac-address string               Container MAC address (e.g., 92:d0:c6:0a:29:33)
-m, --memory bytes                     Memory limit
    --memory-reservation bytes         Memory soft limit
    --memory-swap bytes                Swap limit equal to memory plus swap: '-1' to enable unlimited swap
    --memory-swappiness int            Tune container memory swappiness (0 to 100) (default -1)
    --mount mount                      Attach a filesystem mount to the container
    --name string                      Assign a name to the container
    --network network                  Connect a container to a network
    --network-alias list               Add network-scoped alias for the container
    --no-healthcheck                   Disable any container-specified HEALTHCHECK
    --oom-kill-disable                 Disable OOM Killer
    --oom-score-adj int                Tune host's OOM preferences (-1000 to 1000)
    --pid string                       PID namespace to use
    --pids-limit int                   Tune container pids limit (set -1 for unlimited)
    --platform string                  Set platform if server is multi-platform capable
    --privileged                       Give extended privileges to this container
-p, --publish list                     Publish a container's port(s) to the host
-P, --publish-all                      Publish all exposed ports to random ports
    --pull string                      Pull image before running ("always", "missing", "never") (default "missing")
-q, --quiet                            Suppress the pull output
    --read-only                        Mount the container's root filesystem as read only
    --restart string                   Restart policy to apply when a container exits (default "no")
    --rm                               Automatically remove the container when it exits
    --runtime string                   Runtime to use for this container
    --security-opt list                Security Options
    --shm-size bytes                   Size of /dev/shm
    --sig-proxy                        Proxy received signals to the process (default true)
    --stop-signal string               Signal to stop the container
    --stop-timeout int                 Timeout (in seconds) to stop a container
    --storage-opt list                 Storage driver options for the container
    --sysctl map                       Sysctl options (default map[])
    --tmpfs list                       Mount a tmpfs directory
-t, --tty                              Allocate a pseudo-TTY
    --ulimit ulimit                    Ulimit options (default [])
-u, --user string                      Username or UID (format: <name|uid>[:<group|gid>])
    --userns string                    User namespace to use
    --uts string                       UTS namespace to use
-v, --volume list                      Bind mount a volume
    --volume-driver string             Optional volume driver for the container
    --volumes-from list                Mount volumes from the specified container(s)
-w, --workdir string                   Working directory inside the container
```

</details>

<details>

<summary>docker logs</summary>

* 컨테이너의 로그를 가져온다.

<!---->

* `docker container logs` 의 축약형



### 시놉시스

`docker logs [OPTIONS] CONTAINER`



### 옵션

```
    --details        Show extra details provided to logs
-f, --follow         Follow log output
    --since string   Show logs since timestamp (e.g. "2013-01-02T13:23:37Z") 
                     or relative (e.g. "42m" for 42 minutes)
-n, --tail string    Number of lines to show from the end of the logs (default "all")
-t, --timestamps     Show timestamps
    --until string   Show logs before a timestamp (e.g. "2013-01-02T13:23:37Z") 
                     or relative (e.g. "42m" for 42 minutes)
```

</details>



##
