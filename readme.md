# Run Stable Diffusion Web UI on an EC2 instance using a spot instance with a 70% discount

You will encounter a hurdle when you want to run Stable Diffusion Web UI because, at first, you need GPUs in your computer, which are expensive. A better alternative is using public clouds such as AWS. The pay-as-you-go system enables you to start Stable Diffusion at a cheaper cost, but for the recommended g4dn.xlarge instance, it costs 0.526 USD per hour in the us-east-1 region. However, a spot instance gives you about 70% discount compared to On-Demand prices. Spot instances are unused EC2 capacity in AWS so relatively unstable, but you will not see problems for personal use. 

## Usage

1. Create stacks in CloudFormation by importing `template.yaml`. It prompts you to input your network's global ip CIDR.
2. After finishing it, connect to an instance that has started running using Session Manager.
3. Soon after the instance boots up, the initial scripts will run, and you will need to wait for approximately 10 minutes until you see `Finish.txt` in the root directory. If you can't wait for finish, run `sudo tail -n 1000 -f /var/log/cloud-init-output.log` to see a log for the initial steps.
4. `cd /stable-diffusion-webui` and run `sudo -u ubuntu ./webui.sh`. Or you can add parameters like `sudo -u ubuntu ./webui.sh --listen --xformers`.
5. If you used `--listen`, access your instance's public dns like `ec2-34-205-89-2.compute-1.amazonaws.com:7860`. If you use `--share`, please follow a link shown.

## Caution
Your instance will be put in a public subnet. It will be protected by a security group but connected to the internet directly. You should use this template at your own risk.