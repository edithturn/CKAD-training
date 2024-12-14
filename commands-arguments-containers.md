# Managing command in containers

- args: ["-c", "while true; do date >> /var/log/app.txt; sleep 5; done"]
- args: [/bin/sh, -c, 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done']
- args: ["-c", "mkdir -p collect; while true; do cat /var/data/\*> /collect/data.txt; sleep 10; d
