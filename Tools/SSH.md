- Check of Active Tunnel 
```bash
nc -z localhost 6000 || echo "no tunnel open"
```

- SSH into VM Database
```bash
ssh -L 127.0.0.1:3307:192.168.7.77:3306 polak@192.168.7.82 -N

```

- SSH into Nested VMs
```bash
ssh -J polak@192.168.7.82 root@192.168.7.77
```

- Double Tunnel with Single Command
```bash
ssh -L 127.0.0.1:3309:localhost:3307 -tt polak@192.168.7.82 ssh -L 127.0.0.1:3307:localhost:3306 amir@192.168.7.55

ssh -L 127.0.0.1:3309:localhost:3307 -tt polak@192.168.7.82 ssh -L 127.0.0.1:3307:localhost:3306 amir@192.168.7.55 -N

```

