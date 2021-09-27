# How to manage ASG & ELB on AWS using Terraform & GitHub Actions

### What is GitHub Actions?

GitHub Actions help you automate tasks within your software development life cycle. GitHub Actions are event-driven, meaning that you can run a series of commands after a specified event has occurred. For example, every time someone creates a pull request for a repository or someone merges the code to the repository, you can automatically run a command that executes a software testing script.

![1](https://github.com/DhruvinSoni30/GitHub_Actions-Terraform/blob/main/1.jpeg)

### What is Terraform?

Terraform is a free and open-source infrastructure as code (IAC) that can help to automate the deployment, configuration, and management of the remote servers. Terraform can manage both existing service providers and custom in-house solutions.

![2](https://github.com/DhruvinSoni30/GitHub_Actions-Terraform/blob/main/2.png)

In this tutorial, I have integrated Terraform with GitHub Actions and created various resources on AWS.

![3](https://github.com/DhruvinSoni30/GitHub_Actions-Terraform/blob/main/3.jpeg)

### Prerequisite:

* The GitHub Account
* Basic understanding of Terraform, GitHub Actions & AWS
* An Access key & Secret key created the AWS

Lets, start with the configuration of the project

![Setup](https://github.com/DhruvinSoni30/Terrafrom-ELB-ASG/blob/main/1.png)

![Setup](https://github.com/DhruvinSoni30/Terrafrom-ELB-ASG/blob/main/1.png)

So, now our entire code is ready. We need to create `Workflow` for automation.

* Create `.github/workflows/terraform.yaml` file and add below content to it.
  ```
  name: Terraform-GitHub-Actions

  on:
    push:
      branches: [ main ]
    pull_request:
      branches: [ main ]

  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.aws_access_key }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.aws_secret_key }}

  jobs:
    build:
      name: build
      runs-on: ubuntu-latest
      steps:
        - name: Checkout
          uses: actions/checkout@v2
       
        - name: Set up Terraform
          uses: hashicorp/setup-terraform@v1
      
        - name: Terraform Init
          id: init
          run: terraform init
      
        - name: Terraform Plan
          id: plan
          run: terraform plan
      
        - name: Terraform Apply
          id: apply
          run: terraform apply --auto-approve
  
  ```

* Now, As soon as you commit your workflow file GitHub will trigger the action and the resources will be going to create on the AWS account.

![6](https://github.com/DhruvinSoni30/GitHub_Actions-Terraform/blob/main/6.png)

* After running the job you will see that all the steps run perfectly and there was no error. So you will have a grey color tick mark as each step run successfully.

![7](https://github.com/DhruvinSoni30/GitHub_Actions-Terraform/blob/main/7.png)

* You can also check the output of each step by expanding it

![8](https://github.com/DhruvinSoni30/GitHub_Actions-Terraform/blob/main/8.png)

* Check the resources on AWS
  * VPC
  * Auto Scaling Group
  * Launch Configurationn
  * Auto Scaling Policy
  * Load Balancer
  * Internet Gateway
  * Route Table
  * Security Groups
  * Subnets
  * Cloud Watch Alarm

After the infrastructure is ready you can verify the output by navigating `http://DNS-of-Load-Balancer` you should see the below output.

![Output](https://github.com/DhruvinSoni30/Terrafrom-ELB-ASG/blob/main/2.png)

That’s it now, you have learned how to set up dynamic Auto Scaling Group and Load Balancer to distribute traffic to your instances in multiple Availability Zones. 
