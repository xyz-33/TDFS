# TDFS

## Install

Need to install Golang and Apache Thrift 

run the following line in terminal

```bash
thrift -r --gen go ./thrift/main.thrift
```

## Compile

```bash
go build -o ./out/tdfs.exe ./src/user-client/
go build -o ./out/namenode.exe ./src/namenode-server/
go build -o ./out/datanode.exe ./src/datanode-server/
```

## Execute

### NameNode Server

**Example**

```bash
namenode -port 19100 -limit 2 -interval 30
```
**Parameter Explaination**

| Parameter  | Explaination                                        | Default Value |
| ---------  | ----------------------------------------------------| ------------- |
| -port      | port number when a service start                    | 19100         |
| -limit     | minimum of replicas that system will keep for files | 2             |
| -interval  | interval of heartbeat test for DataNodes            | 30            |
| -h         | help                                                | -             |


### DataNode Server

**Example**

```bash
datanode -nnaddr "localhost:19100" -port 19200 -root "./storage/" -space "1GB"
```

**Parameter Explaination**

| Parameter | Explaination                                    | Default Value     |
| --------  | ----------------------------------------------- | ----------------- |
| -nnaddr   | NameNode's URL                                  | "localhost:19100" |
| -port     | port number when a service start                | 19200             |
| -root     | directory to keep files                         | "./storage/"      |
| -space    | storage space allocated to the DataNode         | "1GB"             |
| -h        | help                                            | -                 |

### Client Side

#### Create configuration 

Under the same directory of `tdfs` client files, create `config.yml`，fill in NameNode address（Currently the system only support single NameNode, so you should fill in just one address）

```yaml
namenode:
  - <host>:<port>
  - <host>:<port>
  - <host>:<port>
```

#### Command

##### `put`

alias：`p`

upload a local file to the tdfs

```bash
tdfs put <local_file_path> <remote_file_path>
```

##### `get`

alias：`g`

download a file from tdfs to a local directory

```bash
tdfs get <remote_file_path> <local_file_path>
```

##### `move`

alias：`mv`, `rename`

rename or move a file on tdfs

```bash
tdfs move <old_file_path> <new_file_path>
```

##### `delete`

alias：`rm`

remove a file on tdfs

```bash
tdfs delete <file_path>
```

##### `stat`

alias：`s`

show file information on tdfs

```bash
tdfs stat <file_path>
```

##### `list`

alias：`ls`

show every files under a certain directory of tdfs

```bash
tdfs list <dir_path>
```

##### `mkdir`

check whether a certain directory is usable

```bash
tdfs mkdir <dir_path>
```

##### `datanodes`

alias：`dn`

show all the connected DataNodes' status

```bash
tdfs datanodes
```

##### `help`

show help

```bash
tdfs help
```
