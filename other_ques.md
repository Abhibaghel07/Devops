

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

