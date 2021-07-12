# Chapter 1 - The Basics

`podman search <image>` -> searches images from remote or local registries

`podman pull <image>` -> downloads the image to save locally 

## Container Images Syntax Name 

```
registry_name/user_name/image_name:tag
 FQDN		   OWNER	   NAME       VERSION
 ```
 
`podman images` -> lists images stored locally 

## Running Containers

`podman run ubi8/ubi:8.3 echo 'Hello World!` -> red hat universal image base entry point echo command

`podman run -d -p 8080 registry.redhat.io/rhel8/httpd-24´ -> run the container as background process (or you will lose terminal session)

- `-p 8080` -> container por binded to a localport 
- `podman port -l` -> list the port tha is used by the container 	- `/bin/bash` -> bash terminal inside the container
	- Example: `podman exec -it <container name or id> /bin/bash`	
- `--rm` -> destroys the container when exited

`podman run -e GREET=Hello -e NAME=Redhat ubi8/ubi8:8.3 printenv GREET NAME` -> some containers needs parameters to run, such as password or username

- Example: `podman run --name mysql -e MYSQL_USER=redhat -e MYSQL_PASSWORD=r3dh4t -d registry.redhat.io/rhel8/mysql-80`
	
## Rootless Containers

Containers that do not require root privileges to run. Code inside can run as root, creates an abstraction layer for possible attacks, isolation and any user can run. 

For Network this poses a problem, because for the create of a virtual ethernet interface you need to be a root user. On rootles containers, Slirp manages the network.

Additionally, FUSE-OverlayFS is used instead of the dafault Overlat2 in rootles containers to create a new storage driver, user-space oriented. This is used because in most linux distros it wont allow overlay files sistems in user namespaces. 
