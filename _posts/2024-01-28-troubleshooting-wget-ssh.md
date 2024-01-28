---
layout: post
title: troubleshooting ssl/tls certificate valiadation issue in wget 
date: 2023-08-30 15:09:00
description: troubleshooting ssl/tls certificate valiadation issue in wget 
tags: troubleshoot
categories: troubleshoot
featured: true
---

If you're encountering the "SSL/TLS certificate is not being validated" issue with the `wget` command, it means that `wget` is not able to verify the SSL/TLS certificate of the server. This could happen for various reasons, and here are some steps you can take to address the issue:

1. **Update `wget`:** Ensure that you are using the latest version of `wget` as newer versions may have bug fixes and improvements.

   ```bash
   sudo apt-get update
   sudo apt-get install wget
   ```

   On other systems, you may need to use the package manager specific to your platform.

2. **Check Certificate Expiry:** Make sure that the SSL/TLS certificate on the server you are trying to connect to is still valid. Certificates have expiration dates, and if the certificate has expired, `wget` will not be able to validate it.

3. **Specify Certificate Authority (CA) File:**
   
   ```bash
   wget --ca-certificate=/path/to/ca-cert-file https://example.com
   ```

   Replace `/path/to/ca-cert-file` with the path to your CA certificate file. This helps `wget` to validate the server's certificate against the provided CA certificate.

4. **Use `--no-check-certificate` (Not Recommended):**
   While this is not recommended for security reasons, you can use the `--no-check-certificate` option to bypass SSL certificate validation.

   ```bash
   wget --no-check-certificate https://example.com
   ```

   This option should only be used in a controlled environment or when you are sure of the security implications.

5. **Check System Date and Time:**
   Ensure that the system date and time on your machine are accurate. If the date and time are incorrect, SSL/TLS certificate validation may fail.

6. **Firewall and Proxy Settings:**
   If you are behind a firewall or using a proxy, make sure that it is configured correctly and not causing interference with the SSL/TLS connection.

Remember that using `--no-check-certificate` compromises security, and it's essential to identify and address the underlying issue causing the certificate validation failure whenever possible.

