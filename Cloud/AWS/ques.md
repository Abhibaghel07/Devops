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
