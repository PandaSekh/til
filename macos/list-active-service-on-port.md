# How to List and Kill Services on a Specific Port in MacOS

On MacOS, to list active services on a specific port (e.g., port 8080), open your terminal and run this command:
```
sudo lsof -i :8080
```

To kill a service on a specific port, first obtain its PID from the lsof output, and then run this command:
```
sudo kill -9 <PID>
```
Replace <PID> with the process ID you obtained from the previous command.

Reference: https://stackoverflow.com/a/72814058