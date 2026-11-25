# Cybersecurity Lab

## 1. Project Overview
This project uses Ubuntu, Docker and DVWA to create a local cybersecurity lab.

## 2. Docker Verification
Command:
```bash
sudo docker --version
sudo docker ps
```

## 3. DVWA
DVWA runs locally on port 8080.

URL: http://127.0.0.1:8080

## 4. Authentication Log
The auth.log file contains five sample failed SSH login entries.

Command:
```bash
cat auth.log
```

## 5. Extract Failed Login Information

### Find failed login attempts
```bash
grep "Failed password" auth.log
```

### Count failed attempts
```bash
grep -c "Failed password" auth.log
```

### Extract usernames, IP addresses and timestamps
```bash
grep "Failed password" auth.log | awk '{
    timestamp = $1 " " $2 " " $3
    username = "unknown"
    ip = "unknown"

    for (i = 1; i <= NF; i++) {
        if ($i == "user" && $(i-1) == "invalid")
            username = $(i+1)
        else if ($i == "for" && $(i+1) != "invalid")
            username = $(i+1)

        if ($i == "from")
            ip = $(i+1)
    }

    print "Timestamp:", timestamp
    print "Username:", username
    print "IP Address:", ip
    print "----------------------"
}'
```

## 6. Conclusion
Successfully created a local DVWA environment using Docker and practiced basic Linux log analysis using grep and awk.
