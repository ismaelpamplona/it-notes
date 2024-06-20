Run the following command to find the process ID (PID) of the service running on port 3000:

```sh
sudo lsof -i :3000
```

Run the following command to kill the process, replacing <PID> with the process ID:

```sh
kill -9 <PID>
```
