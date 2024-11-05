1. Deploy the stack
2. use two way console to enter any of the containers
3. enter the following command
    * `redis-cli --cluster create IP:PORT (for each node) --cluster-replicas 0`
        * yes this cluster doesn't have replicas but Im sure you can add them I just wanted to test this with only three nodes for brevity.
4. Give permission for the instance to write config as prompted
5. after cluster meet is successful log out of terminal session
6. log into another node and enter the redis cli with redis-cli
7. run CLUSTER INFO and or CLUSTER NODES to prove that the configuration has been accepted by not just the original node



## Adding Replicas
The above creates a 3 node cluster without replicas.  Read reps can be added, per docs it is:

```bash
redis-cli --cluster add-node <new-node-ip>:<new-node-port> <existing-master-node-ip>:<existing-master-node-port> --cluster-slave
```


## Testing the clustering 

Log in with two-way console and `for i in {1..100}; do redis-cli -c SET key$i "value$i"; done`

Then from any instance run `cluster keyslot 50` or any number between 1-100. 

To see which shard has that keyslot run `cluster nodes`.

