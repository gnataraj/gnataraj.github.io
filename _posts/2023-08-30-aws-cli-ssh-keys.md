---
layout: post
title: a post with code
date: 2023-08-30 15:09:00
description: Using aws-cli to generate ssh-key 
tags: formatting code
categories: sample-posts
featured: true
---
To create an SSH key pair using the AWS Command Line Interface (CLI) and store it in a PPK (PuTTY Private Key) file, you can follow these steps:

1. **Install AWS CLI**: If you haven't already, you'll need to install the AWS CLI on your local machine. You can download it from the [official AWS CLI website](https://aws.amazon.com/cli/).

2. **Configure AWS CLI**: Before you can use the AWS CLI, you need to configure it with your AWS credentials. You can do this by running the `aws configure` command and providing your AWS Access Key ID, Secret Access Key, default region, and output format.

3. **Generate SSH Key Pair**: You can use the `aws ec2 create-key-pair` command to generate an SSH key pair. Here's an example:

   ```bash
   aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
   ```

   - `--key-name MyKeyPair`: Replace "MyKeyPair" with a name for your key pair.
   - `--query 'KeyMaterial' --output text`: This part of the command extracts the private key material and saves it in a file.

4. **Convert the PEM Key to PPK**: AWS generates the private key in PEM format, but if you plan to use it with PuTTY, you'll need to convert it to PPK format. You can use a tool like PuTTYgen to do this:
   
   - Open PuTTYgen.
   - Click "Conversions" in the top menu.
   - Select "Import Key" and choose the `MyKeyPair.pem` file generated in step 3.
   - Click "Save Private Key" to save it in PPK format.

Now you have your SSH key pair stored in a PPK file, which you can use with PuTTY or other SSH clients that support PPK files.

Remember to keep your private key secure, as it provides access to your AWS resources. Also, make sure your AWS CLI is properly configured with the necessary IAM permissions to perform these operations.
