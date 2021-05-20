## Readiness and Liveness Probes

Pod -> status and conditions.







### Readiness Probe

```yaml
radinessProbe:
    httpGet:
        path: /api/ready
        port: 8080
    initialDelaySeconds: 10
    periodSeconds: 5
    failireThreshold: 8
```


```yaml
radinessProbe:
    tcpSocket:
        port: 8080
```

```yaml
radinessProbe:
    exec:
        command:
            - cat
            - /app/is_ready
```

### leaviness Probe

http test - /api/ready
```yaml
livenessProbe:
    httpGet:
        path: /api/healthy
        port: 8080
    initialDelaySeconds: 10
    periodSeconds: 5
    failireThreshold: 8
```

TCP Test - 3306

```yaml
livenessProbe:
    tcpSocket:
        port: 3306
```

Exec Command
```yaml
livenessProbe:
    exec:
        command:
            - cat
            - /app/is_healthy
```

