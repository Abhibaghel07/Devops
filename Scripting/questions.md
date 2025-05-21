
## 🔧 **Linux System Administration and Troubleshooting**

1. **Q: How do you check disk usage on a Linux server?**
   **A:** Use `df -h` for disk usage by mount point and `du -sh /path` for folder-specific usage.

2. **Q: How can you monitor memory and CPU usage?**
   **A:** Use `top`, `htop`, `free -m`, or `vmstat`.

3. **Q: How do you check system logs?**
   **A:** Logs are in `/var/log/`, e.g., `syslog`, `messages`, `dmesg`, and can be viewed using `cat`, `less`, or `journalctl`.

4. **Q: How do you restart a failed service in Linux?**
   **A:** Use `systemctl restart service_name` and check status with `systemctl status`.

5. **Q: How do you find large files in Linux?**
   **A:** `find / -type f -size +500M -exec ls -lh {} \;`

6. **Q: What command shows active network connections?**
   **A:** `netstat -tunlp`, `ss -tuln`

7. **Q: How do you troubleshoot a system that is unresponsive?**
   **A:** Check CPU/memory (`top`), I/O wait (`iostat`), disk (`df`), logs (`journalctl`, `/var/log/messages`).

8. **Q: How do you check which process is using the most memory?**
   **A:** Use `top`, sort by memory, or `ps aux --sort=-%mem | head`.

---

## 🐚 **Bash/Shell Scripting**

9. **Q: How do you write a loop in Bash?**
   **A:**

   ```bash
   for i in {1..5}; do echo $i; done
   ```

10. **Q: How do you pass arguments to a script?**
    **A:** Using `$1`, `$2`, etc. in the script.

11. **Q: How do you handle errors in a shell script?**
    **A:** Use `set -e`, `trap`, and check `$?` after commands.

12. **Q: How do you read a file line by line in Bash?**
    **A:**

    ```bash
    while IFS= read -r line; do echo "$line"; done < file.txt
    ```

13. **Q: How do you schedule a script to run every day?**
    **A:** Use `crontab -e`, e.g., `0 0 * * * /path/to/script.sh`

14. **Q: Write a script to find and delete `.log` files older than 7 days.**

    ```bash
    find /var/log -name "*.log" -type f -mtime +7 -exec rm -f {} \;
    ```

15. **Q: How do you debug a shell script?**
    **A:** Use `bash -x script.sh` or add `set -x` at the top.

---

## 🐍 **Python for Automation**

16. **Q: How do you read a file in Python?**

    ```python
    with open('file.txt') as f:
        data = f.read()
    ```

17. **Q: How do you execute a shell command in Python?**

    ```python
    import subprocess
    subprocess.run(['ls', '-l'])
    ```

18. **Q: How do you use boto3 to list S3 buckets?**

    ```python
    import boto3
    s3 = boto3.client('s3')
    for bucket in s3.list_buckets()['Buckets']:
        print(bucket['Name'])
    ```

19. **Q: How do you parse JSON in Python?**

    ```python
    import json
    data = json.loads('{"key": "value"}')
    ```

20. **Q: How do you handle exceptions in Python?**

    ```python
    try:
        risky_operation()
    except Exception as e:
        print(f"Error: {e}")
    ```

21. **Q: How do you schedule periodic tasks in Python?**
    **A:** Use `schedule`, `cron`, or external schedulers like `Celery`.

22. **Q: How do you write a REST API caller in Python?**

    ```python
    import requests
    r = requests.get('https://api.example.com')
    print(r.json())
    ```

---