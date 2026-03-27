
## Terminate a process by port
```sh
netstat -ano | findstr :3000

# output TCP    0.0.0.0:3000     0.0.0.0:0      LISTENING      12345
taskkill /PID 12345 /F
```