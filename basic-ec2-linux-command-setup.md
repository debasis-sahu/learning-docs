## Connecting to EC2 (Most Important)

To SSH into your EC2 instance:
```sh
ssh -i your-key.pem ec2-user@<EC2_PUBLIC_IP>
```

If you get a "Permission denied" error regarding your private key, run:
```sh
chmod 400 your-key.pem
```