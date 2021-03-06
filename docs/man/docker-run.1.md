% DOCKER(1) Docker User Manuals
% Docker Community
% JUNE 2014
# NAME
docker-run - Run a command in a new container

# SYNOPSIS
**docker run**
[**-a**|**--attach**[=*[]*]]
[**--add-host**[=*[]*]]
[**-c**|**--cpu-shares**[=*0*]]
[**--cap-add**[=*[]*]]
[**--cap-drop**[=*[]*]]
[**--cidfile**[=*CIDFILE*]]
[**--cpuset**[=*CPUSET*]]
[**-d**|**--detach**[=*false*]]
[**--device**[=*[]*]]
[**--dns-search**[=*[]*]]
[**--dns**[=*[]*]]
[**-e**|**--env**[=*[]*]]
[**--entrypoint**[=*ENTRYPOINT*]]
[**--env-file**[=*[]*]]
[**--expose**[=*[]*]]
[**-h**|**--hostname**[=*HOSTNAME*]]
[**-i**|**--interactive**[=*false*]]
[**--ipc**[=*IPC*]]
[**--link**[=*[]*]]
[**--lxc-conf**[=*[]*]]
[**-m**|**--memory**[=*MEMORY*]]
[**--mac-address**[=*MAC-ADDRESS*]]
[**--name**[=*NAME*]]
[**--net**[=*"bridge"*]]
[**-P**|**--publish-all**[=*false*]]
[**-p**|**--publish**[=*[]*]]
[**--privileged**[=*false*]]
[**--restart**[=*RESTART*]]
[**--rm**[=*false*]]
[**--security-opt**[=*[]*]]
[**--sig-proxy**[=*true*]]
[**-t**|**--tty**[=*false*]]
[**-u**|**--user**[=*USER*]]
[**-v**|**--volume**[=*[]*]]
[**--volumes-from**[=*[]*]]
[**-w**|**--workdir**[=*WORKDIR*]]
IMAGE [COMMAND] [ARG...]

# DESCRIPTION

Run a process in a new container. **docker run** starts a process with its own
file system, its own networking, and its own isolated process tree. The IMAGE
which starts the process may define defaults related to the process that will be
run in the container, the networking to expose, and more, but **docker run**
gives final control to the operator or administrator who starts the container
from the image. For that reason **docker run** has more options than any other
Docker command.

If the IMAGE is not already loaded then **docker run** will pull the IMAGE, and
all image dependencies, from the repository in the same way running **docker
pull** IMAGE, before it starts the container from that image.

# OPTIONS
**-a**, **--attach**=[]
   Attach to STDIN, STDOUT or STDERR.

   In foreground mode (the default when **-d**
is not specified), **docker run** can start the process in the container
and attach the console to the process’s standard input, output, and standard
error. It can even pretend to be a TTY (this is what most commandline
executables expect) and pass along signals. The **-a** option can be set for
each of stdin, stdout, and stderr.

**--add-host**=[]
   Add a custom host-to-IP mapping (host:ip)

   Add a line to /etc/hosts. The format is hostname:ip.  The **--add-host**
option can be set multiple times.

**-c**, **--cpu-shares**=0
   CPU shares (relative weight)

   You can increase the priority of a container
with the -c option. By default, all containers run at the same priority and get
the same proportion of CPU cycles, but you can tell the kernel to give more
shares of CPU time to one or more containers when you start them via **docker
run**.

**--cap-add**=[]
   Add Linux capabilities

**--cap-drop**=[]
   Drop Linux capabilities

**--cidfile**=""
   Write the container ID to the file

**--cpuset**=""
   CPUs in which to allow execution (0-3, 0,1)

**-d**, **--detach**=*true*|*false*
   Detached mode: run the container in the background and print the new container ID. The default is *false*.

   At any time you can run **docker ps** in
the other shell to view a list of the running containers. You can reattach to a
detached container with **docker attach**. If you choose to run a container in
the detached mode, then you cannot use the **-rm** option.

   When attached in the tty mode, you can detach from a running container without
stopping the process by pressing the keys CTRL-P CTRL-Q.

**--device**=[]
   Add a host device to the container (e.g. --device=/dev/sdc:/dev/xvdc:rwm)

**--dns-search**=[]
   Set custom DNS search domains (Use --dns-search=. if you don't wish to set the search domain)

**--dns**=[]
   Set custom DNS servers

   This option can be used to override the DNS
configuration passed to the container. Typically this is necessary when the
host DNS configuration is invalid for the container (e.g., 127.0.0.1). When this
is the case the **--dns** flags is necessary for every run.

**-e**, **--env**=[]
   Set environment variables

   This option allows you to specify arbitrary
environment variables that are available for the process that will be launched
inside of the container.

**--entrypoint**=""
   Overwrite the default ENTRYPOINT of the image

   This option allows you to overwrite the default entrypoint of the image that
is set in the Dockerfile. The ENTRYPOINT of an image is similar to a COMMAND
because it specifies what executable to run when the container starts, but it is
(purposely) more difficult to override. The ENTRYPOINT gives a container its
default nature or behavior, so that when you set an ENTRYPOINT you can run the
container as if it were that binary, complete with default options, and you can
pass in more options via the COMMAND. But, sometimes an operator may want to run
something else inside the container, so you can override the default ENTRYPOINT
at runtime by using a **--entrypoint** and a string to specify the new
ENTRYPOINT.

**--env-file**=[]
   Read in a line delimited file of environment variables

**--expose**=[]
   Expose a port, or a range of ports (e.g. --expose=3300-3310), from the container without publishing it to your host

**-h**, **--hostname**=""
   Container host name

   Sets the container host name that is available inside the container.

**-i**, **--interactive**=*true*|*false*
   Keep STDIN open even if not attached. The default is *false*.

   When set to true, keep stdin open even if not attached. The default is false.

**--ipc**=""
   Default is to create a private IPC namespace (POSIX SysV IPC) for the container
                               'container:<name|id>': reuses another container shared memory, semaphores and message queues
                               'host': use the host shared memory,semaphores and message queues inside the container.  Note: the host mode gives the container full access to local shared memory and is therefore considered insecure.

**--link**=[]
   Add link to another container in the form of name:alias

   If the operator
uses **--link** when starting the new client container, then the client
container can access the exposed port via a private networking interface. Docker
will set some environment variables in the client container to help indicate
which interface and port to use.

**--lxc-conf**=[]
   (lxc exec-driver only) Add custom lxc options --lxc-conf="lxc.cgroup.cpuset.cpus = 0,1"

**-m**, **--memory**=""
   Memory limit (format: <number><optional unit>, where unit = b, k, m or g)

   Allows you to constrain the memory available to a container. If the host
supports swap memory, then the -m memory setting can be larger than physical
RAM. If a limit of 0 is specified, the container's memory is not limited. The
actual limit may be rounded up to a multiple of the operating system's page
size, if it is not already. The memory limit should be formatted as follows:
`<number><optional unit>`, where unit = b, k, m or g.

**--mac-address**=""
   Container MAC address (e.g. 92:d0:c6:0a:29:33)

   Remember that the MAC address in an Ethernet network must be unique.
The IPv6 link-local address will be based on the device's MAC address
according to RFC4862.

**--name**=""
   Assign a name to the container

   The operator can identify a container in three ways:
    UUID long identifier (“f78375b1c487e03c9438c729345e54db9d20cfa2ac1fc3494b6eb60872e74778”)
    UUID short identifier (“f78375b1c487”)
    Name (“jonah”)

   The UUID identifiers come from the Docker daemon, and if a name is not assigned
to the container with **--name** then the daemon will also generate a random
string name. The name is useful when defining links (see **--link**) (or any
other place you need to identify a container). This works for both background
and foreground Docker containers.

**--net**="bridge"
   Set the Network mode for the container
                               'bridge': creates a new network stack for the container on the docker bridge
                               'none': no networking for this container
                               'container:<name|id>': reuses another container network stack
                               'host': use the host network stack inside the container.  Note: the host mode gives the container full access to local system services such as D-bus and is therefore considered insecure.

**-P**, **--publish-all**=*true*|*false*
   Publish all exposed ports to the host interfaces. The default is *false*.

   When set to true publish all exposed ports to the host interfaces. The
default is false. If the operator uses -P (or -p) then Docker will make the
exposed port accessible on the host and the ports will be available to any
client that can reach the host. When using -P, Docker will bind the exposed
ports to a random port on the host between 49153 and 65535. To find the
mapping between the host ports and the exposed ports, use **docker port**.

**-p**, **--publish**=[]
   Publish a container's port, or range of ports, to the host.
                               format: ip:hostPort:containerPort | ip::containerPort | hostPort:containerPort | containerPort
                               Both hostPort and containerPort can be specified as a range of ports. 
                               When specifying ranges for both, the number of container ports in the range must match the number of host ports in the range. (e.g., `-p 1234-1236:1234-1236/tcp`)
                               (use 'docker port' to see the actual mapping)

**--privileged**=*true*|*false*
   Give extended privileges to this container. The default is *false*.

   By default, Docker containers are
“unprivileged” (=false) and cannot, for example, run a Docker daemon inside the
Docker container. This is because by default a container is not allowed to
access any devices. A “privileged” container is given access to all devices.

   When the operator executes **docker run --privileged**, Docker will enable access
to all devices on the host as well as set some configuration in AppArmor to
allow the container nearly all the same access to the host as processes running
outside of a container on the host.

**--restart**=""
   Restart policy to apply when a container exits (no, on-failure[:max-retry], always)

**--rm**=*true*|*false*
   Automatically remove the container when it exits (incompatible with -d). The default is *false*.

**--security-opt**=[]
   Security Options

   "label:user:USER"   : Set the label user for the container
    "label:role:ROLE"   : Set the label role for the container
    "label:type:TYPE"   : Set the label type for the container
    "label:level:LEVEL" : Set the label level for the container
    "label:disable"     : Turn off label confinement for the container

**--sig-proxy**=*true*|*false*
   Proxy received signals to the process (non-TTY mode only). SIGCHLD, SIGSTOP, and SIGKILL are not proxied. The default is *true*.

**-t**, **--tty**=*true*|*false*
   Allocate a pseudo-TTY. The default is *false*.

   When set to true Docker can allocate a pseudo-tty and attach to the standard
input of any container. This can be used, for example, to run a throwaway
interactive shell. The default is value is false.

The **-t** option is incompatible with a redirection of the docker client
standard input.

**-u**, **--user**=""
   Username or UID

**-v**, **--volume**=[]
   Bind mount a volume (e.g., from the host: -v /host:/container, from Docker: -v /container)

   The **-v** option can be used one or
more times to add one or more mounts to a container. These mounts can then be
used in other containers using the **--volumes-from** option.

   The volume may be optionally suffixed with :ro or :rw to mount the volumes in
read-only or read-write mode, respectively. By default, the volumes are mounted
read-write. See examples.

**--volumes-from**=[]
   Mount volumes from the specified container(s)

   Will mount volumes from the specified container identified by container-id.
Once a volume is mounted in a one container it can be shared with other
containers using the **--volumes-from** option when running those other
containers. The volumes can be shared even if the original container with the
mount is not running.

   The container ID may be optionally suffixed with :ro or
:rw to mount the volumes in read-only or read-write mode, respectively. By
default, the volumes are mounted in the same mode (read write or read only) as
the reference container.

**-w**, **--workdir**=""
   Working directory inside the container

   The default working directory for
running binaries within a container is the root directory (/). The developer can
set a different default with the Dockerfile WORKDIR instruction. The operator
can override the working directory by using the **-w** option.

# EXAMPLES

## Exposing log messages from the container to the host's log

If you want messages that are logged in your container to show up in the host's
syslog/journal then you should bind mount the /dev/log directory as follows.

    # docker run -v /dev/log:/dev/log -i -t fedora /bin/bash

From inside the container you can test this by sending a message to the log.

    (bash)# logger "Hello from my container"

Then exit and check the journal.

    # exit

    # journalctl -b | grep Hello

This should list the message sent to logger.

## Attaching to one or more from STDIN, STDOUT, STDERR

If you do not specify -a then Docker will attach everything (stdin,stdout,stderr)
. You can specify to which of the three standard streams (stdin, stdout, stderr)
you’d like to connect instead, as in:

    # docker run -a stdin -a stdout -i -t fedora /bin/bash

## Sharing IPC between containers

Using shm_server.c available here: http://www.cs.cf.ac.uk/Dave/C/node27.html

Testing `--ipc=host` mode:

Host shows a shared memory segment with 7 pids attached, happens to be from httpd:

```
 $ sudo ipcs -m

 ------ Shared Memory Segments --------
 key        shmid      owner      perms      bytes      nattch     status      
 0x01128e25 0          root       600        1000       7                       
```

Now run a regular container, and it correctly does NOT see the shared memory segment from the host:

```
 $ sudo docker run -it shm ipcs -m

 ------ Shared Memory Segments --------	
 key        shmid      owner      perms      bytes      nattch     status      
```

Run a container with the new `--ipc=host` option, and it now sees the shared memory segment from the host httpd:

 ```
 $ sudo docker run -it --ipc=host shm ipcs -m

 ------ Shared Memory Segments --------
 key        shmid      owner      perms      bytes      nattch     status      
 0x01128e25 0          root       600        1000       7                   
```
Testing `--ipc=container:CONTAINERID` mode:

Start a container with a program to create a shared memory segment:
```
 sudo docker run -it shm bash
 $ sudo shm/shm_server &
 $ sudo ipcs -m

 ------ Shared Memory Segments --------
 key        shmid      owner      perms      bytes      nattch     status      
 0x0000162e 0          root       666        27         1                       
```
Create a 2nd container correctly shows no shared memory segment from 1st container:
```
 $ sudo docker run shm ipcs -m

 ------ Shared Memory Segments --------
 key        shmid      owner      perms      bytes      nattch     status      
```

Create a 3rd container using the new --ipc=container:CONTAINERID option, now it shows the shared memory segment from the first:

```
 $ sudo docker run -it --ipc=container:ed735b2264ac shm ipcs -m
 $ sudo ipcs -m

 ------ Shared Memory Segments --------
 key        shmid      owner      perms      bytes      nattch     status      
 0x0000162e 0          root       666        27         1
```

## Linking Containers

The link feature allows multiple containers to communicate with each other. For
example, a container whose Dockerfile has exposed port 80 can be run and named
as follows:

    # docker run --name=link-test -d -i -t fedora/httpd

A second container, in this case called linker, can communicate with the httpd
container, named link-test, by running with the **--link=<name>:<alias>**

    # docker run -t -i --link=link-test:lt --name=linker fedora /bin/bash

Now the container linker is linked to container link-test with the alias lt.
Running the **env** command in the linker container shows environment variables
 with the LT (alias) context (**LT_**)

    # env
    HOSTNAME=668231cb0978
    TERM=xterm
    LT_PORT_80_TCP=tcp://172.17.0.3:80
    LT_PORT_80_TCP_PORT=80
    LT_PORT_80_TCP_PROTO=tcp
    LT_PORT=tcp://172.17.0.3:80
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    LT_NAME=/linker/lt
    SHLVL=1
    HOME=/
    LT_PORT_80_TCP_ADDR=172.17.0.3
    _=/usr/bin/env

When linking two containers Docker will use the exposed ports of the container
to create a secure tunnel for the parent to access.


## Mapping Ports for External Usage

The exposed port of an application can be mapped to a host port using the **-p**
flag. For example, a httpd port 80 can be mapped to the host port 8080 using the
following:

    # docker run -p 8080:80 -d -i -t fedora/httpd

## Creating and Mounting a Data Volume Container

Many applications require the sharing of persistent data across several
containers. Docker allows you to create a Data Volume Container that other
containers can mount from. For example, create a named container that contains
directories /var/volume1 and /tmp/volume2. The image will need to contain these
directories so a couple of RUN mkdir instructions might be required for you
fedora-data image:

    # docker run --name=data -v /var/volume1 -v /tmp/volume2 -i -t fedora-data true
    # docker run --volumes-from=data --name=fedora-container1 -i -t fedora bash

Multiple --volumes-from parameters will bring together multiple data volumes from
multiple containers. And it's possible to mount the volumes that came from the
DATA container in yet another container via the fedora-container1 intermediary
container, allowing to abstract the actual data source from users of that data:

    # docker run --volumes-from=fedora-container1 --name=fedora-container2 -i -t fedora bash

## Mounting External Volumes

To mount a host directory as a container volume, specify the absolute path to
the directory and the absolute path for the container directory separated by a
colon:

    # docker run -v /var/db:/data1 -i -t fedora bash

When using SELinux, be aware that the host has no knowledge of container SELinux
policy. Therefore, in the above example, if SELinux policy is enforced, the
`/var/db` directory is not writable to the container. A "Permission Denied"
message will occur and an avc: message in the host's syslog.


To work around this, at time of writing this man page, the following command
needs to be run in order for the proper SELinux policy type label to be attached
to the host directory:

    # chcon -Rt svirt_sandbox_file_t /var/db


Now, writing to the /data1 volume in the container will be allowed and the
changes will also be reflected on the host in /var/db.

## Using alternative security labeling

You can override the default labeling scheme for each container by specifying
the `--security-opt` flag. For example, you can specify the MCS/MLS level, a
requirement for MLS systems. Specifying the level in the following command
allows you to share the same content between containers.

    # docker run --security-opt label:level:s0:c100,c200 -i -t fedora bash

An MLS example might be:

    # docker run --security-opt label:level:TopSecret -i -t rhel7 bash

To disable the security labeling for this container versus running with the
`--permissive` flag, use the following command:

    # docker run --security-opt label:disable -i -t fedora bash

If you want a tighter security policy on the processes within a container,
you can specify an alternate type for the container. You could run a container
that is only allowed to listen on Apache ports by executing the following
command:

    # docker run --security-opt label:type:svirt_apache_t -i -t centos bash

Note:

You would have to write policy defining a `svirt_apache_t` type.

# HISTORY
April 2014, Originally compiled by William Henry (whenry at redhat dot com)
based on docker.com source material and internal work.
June 2014, updated by Sven Dowideit <SvenDowideit@home.org.au>
July 2014, updated by Sven Dowideit <SvenDowideit@home.org.au>
