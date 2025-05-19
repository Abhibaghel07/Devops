
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

## ☁️ **AWS**

23. **Q: How do you create an EC2 instance using the AWS CLI?**

    ```bash
    aws ec2 run-instances --image-id ami-xxx --count 1 --instance-type t2.micro --key-name myKey --security-groups mySG
    ```

24. **Q: What is the difference between an IAM Role and IAM User?**
    **A:** Users are for people, roles are for services/instances.

25. **Q: What is the purpose of Security Groups?**
    **A:** Virtual firewalls to control inbound/outbound traffic.

26. **Q: What are the different types of storage in AWS?**
    **A:** S3 (object), EBS (block), EFS (file)

27. **Q: How do you monitor AWS resources?**
    **A:** Use CloudWatch for logs, metrics, and alerts.

28. **Q: What is an Auto Scaling Group?**
    **A:** Automatically adjusts the number of EC2 instances based on load.

29. **Q: How do you connect to a private EC2 instance?**
    **A:** Use a bastion host or Systems Manager Session Manager.

30. **Q: How do you automate AWS tasks?**
    **A:** Use Lambda, CloudFormation, or boto3 scripts.

---

## ⚙️ **Ansible & SaltStack**

31. **Q: What is a playbook in Ansible?**
    **A:** YAML file defining automation steps using tasks and modules.

32. **Q: What is an inventory file?**
    **A:** File listing hosts Ansible will manage.

33. **Q: How do you run a playbook?**

    ```bash
    ansible-playbook playbook.yml -i inventory
    ```

34. **Q: What is a role in Ansible?**
    **A:** A way to group tasks, vars, templates into reusable components.

35. **Q: How do you use variables in Ansible?**
    **A:** Defined in `vars` block, passed via CLI, or inventory.

36. **Q: What is SaltStack?**
    **A:** Configuration management tool using YAML state files.

37. **Q: How do SaltStack states work?**
    **A:** States declare the desired state of resources.

38. **Q: Difference between Ansible and SaltStack?**
    **A:** Ansible is agentless; SaltStack uses agents (minions).

---

## 🌐 **Networking (DNS, OSI Model)**

39. **Q: What are the 7 layers of the OSI model?**
    **A:** Physical, Data Link, Network, Transport, Session, Presentation, Application

40. **Q: How does DNS work?**
    **A:** Client queries DNS resolver → root → TLD → authoritative DNS → IP returned.

41. **Q: What is the difference between TCP and UDP?**
    **A:** TCP is connection-oriented; UDP is faster, connectionless.

42. **Q: What tools do you use for network troubleshooting?**
    **A:** `ping`, `traceroute`, `dig`, `netstat`, `tcpdump`, `ss`

43. **Q: What is NAT?**
    **A:** Network Address Translation – maps private IPs to public IPs.

44. **Q: How do you troubleshoot DNS issues?**
    **A:** Use `dig`, `nslookup`, check `/etc/resolv.conf`, try alternate DNS.

---

## 🧠 **DevOps Tools & Concepts**

45. **Q: What is CI/CD?**
    **A:** Continuous Integration and Continuous Delivery/Deployment for automating testing and releases.

46. **Q: What is Infrastructure as Code?**
    **A:** Managing infrastructure using code (e.g., Terraform, CloudFormation).

47. **Q: What is the role of Docker in DevOps?**
    **A:** Containers ensure consistency across dev, test, and prod.

48. **Q: What are some monitoring tools you’ve used?**
    **A:** Prometheus, Grafana, ELK Stack, CloudWatch.

49. **Q: What is blue-green deployment?**
    **A:** Deploying to a "green" environment while "blue" is active, then switching traffic.

50. **Q: How do you ensure high availability in deployment?**
    **A:** Use load balancers, multi-AZ, auto-scaling, health checks.

51. **Q: How do you manage secrets in a CI/CD pipeline?**
    **A:** Use vaults, environment variables, or secret managers (AWS Secrets Manager).

---

## 🔐 **Secure Communication (SSH, SSL, SFTP)**

52. **Q: How do you set up key-based SSH authentication?**
    **A:** Generate key (`ssh-keygen`), copy public key to `~/.ssh/authorized_keys`.

53. **Q: How do you disable root SSH login?**
    **A:** Edit `/etc/ssh/sshd_config`: `PermitRootLogin no`

54. **Q: What is SFTP and how is it different from FTP?**
    **A:** SFTP uses SSH for secure transfer, FTP is unencrypted.

55. **Q: How do you verify SSL certificates from the command line?**
    **A:** `openssl s_client -connect host:443`

56. **Q: How do you copy files over SSH?**
    **A:** Use `scp file user@host:/path/`

---

## 🧠 **Problem-Solving & Situational**

57. **Q: Describe a time you fixed a critical outage.**
    **A:** \[Prepare your STAR story]

58. **Q: How would you troubleshoot a slow website?**
    **A:** Check server CPU/RAM, analyze logs, use `curl -w`, check app/database performance.

59. **Q: A deployment fails — how do you handle it?**
    **A:** Check logs, roll back if needed, identify root cause, prevent recurrence.

60. **Q: You get a high CPU alert — what next?**
    **A:** Use `top`, `ps`, identify processes, check logs, mitigate (restart/service fix).

61. **Q: Your automation failed mid-run — what do you do?**
    **A:** Check logs, validate partial state, rerun idempotent scripts, ensure retry logic.

---

## 🔄 **Extra / Bonus Questions**

62. **Q: What’s the difference between load balancer and reverse proxy?**
63. **Q: How do containers differ from VMs?**
64. **Q: What is idempotence in Ansible?**
65. **Q: What is the purpose of `.ssh/known_hosts`?**
66. **Q: How does a reverse DNS lookup work?**
67. **Q: What’s the difference between symmetric and asymmetric encryption?**
68. **Q: How would you secure an EC2 instance?**
69. **Q: What is the use of `/etc/hosts` file?**
70. **Q: How do you troubleshoot application-level issues?**
71. **Q: What is a runlevel in Linux?**
72. **Q: How do you check open ports on a server?**
73. **Q: How does `curl` help in debugging APIs?**
74. **Q: What is the difference between `scp` and `rsync`?**
75. **Q: What would you do if you find a security vulnerability in production?**

