# Context

The goal of this lab is to help pentesters learn how to conduct a phishing campaign using GoPhish and Evilginx. It covers SMTP relay service configuration, GoPhish and Evilginx installation and configuration, domain name and VPS purchase, TLS certificate configuration, and defensive measures to detect a phishing website.  

# Table of Contents

- [Phishing Campaign Preparation](#phishing-campaign-preparation)
- [Domain Name Purchase](#domain-name-purchase)
- [VPS Purchase](#vps-purchase)
   * [VPS Configuration](#vps-configuration)
- [GoPhish](#gophish)
   * [Installation](#installation)
   * [Configuration](#configuration)
      + [Firewall Rules](#firewall-rules)
      + [SMTP Relay Service](#smtp-relay-service)
      + [Admin Panel Server](#admin-panel-server)
      + [Phishing Server](#phishing-server)
      + [TLS Certificate](#tls-certificate)
      + [Sending Profiles](#sending-profiles)
      + [Email Templates](#email-templates)
      + [Landing Pages](#landing-pages)
      + [Users & Groups](#users-groups)
      + [Campaigns](#campaigns)
- [Evilginx Community](#evilginx-community)
   * [Installation and Configuration](#installation-and-configuration)
   * [Phishlets](#phishlets)
   * [Lures](#lures)
   * [Sessions](#sessions)
- [GoPhish x Evilginx](#gophish-x-evilginx)
- [Pitfalls to avoid during a phishing campaign](#pitfalls-to-avoid-during-a-phishing-campaign)
- [Tips and Tricks](#tips-and-tricks)
- [Resources](#resources)
- [Disclaimer](#disclaimer)


# Phishing Campaign Preparation

A phishing campaign is a simulated cyberattack that consists of tricking users into revealing sensitive data or perform dangerous actions, such as downloading and installing malicious attachments, which can lead to their account or system compromise. The goal of this assessment is to test how well users respond to fraudulent emails and raise their awareness by providing them with tips to detect those emails.  

Here are some steps that can help you conduct a successful phishing campaign:  

1- Perform technical enumeration such as directory fuzzing, subdomains and vhosts fuzzing, WHOIS and DNS records enumeration. The goal here is to identify the internal and third-party applications used by employees.  
2- Perform some basic OSINT (Open Source Intelligence) such as gathering employees' usernames, emails, and leaked credentials. This step can be taken further by checking employees' social media activity and their interests for spear phishing scenarios.  
3- Purchase and configure your phishing domain name.  
4- Choose an email delivery system or SMTP relay service (Google Workspace, Mailgun, Mailtrap, SendGrid, etc.) for sending your emails. The advantage of using well-known email providers is that they already have a strong reputation, which can help you evade spam filters.  
5- Configure Evilginx or GoPhish to host your phishing website and capture credentials.  
6- Launch your phishing campaign.  
7- Raise employees' awareness and provide technical recommendations to reduce the impact of phishing attacks.  

It is important to understand your client's needs. For instance, make sure you understand the goal and type of phishing campaign (mass phishing campaign, spear phishing campaign, whaling phishing campaign) they want. This will help you conduct a better assessment and provide value to them.  

# Domain Name Purchase

To purchase a domain name you can use [Namecheap](https://www.namecheap.com/domains/).  

**1/ Enter a domain name without the TLD**  

As you can see below, I entered **phishlab** in the search bar, and Namecheap returned some results like `phishlab.inc`, `phishlab.online`, etc.  

<img width="1060" height="749" alt="image" src="https://github.com/user-attachments/assets/94e2492f-652c-4757-ab46-09ac11865f3c" />

Depending on your budget, add a domain name to your cart, then follow the next instructions.  

**2/ Confirm the order**  

Before confirming your order, make sure you disable the **auto-renew** option for your domain. If enabled, this will automatically renew your subscription. Once done, click on `Confirm Order`.  

<img width="1356" height="647" alt="image" src="https://github.com/user-attachments/assets/99295cc6-0753-4bbd-9a3b-ef8480cc0308" />

<br></br>

**3/ Enter your credit card information and purchase your domain**  

The final step consists of purchasing your domain name after entering your credit card information.  
Moreover do not select any additional options if not required. Once done, click on `Continue`.  

<img width="1341" height="636" alt="image" src="https://github.com/user-attachments/assets/e082ae3b-2aa3-430a-a2c6-77d3929a7ef9" />

<br></br>

**4/ Access your purchased domain**  

Here is how to access your domain:  

<img width="1372" height="496" alt="image" src="https://github.com/user-attachments/assets/7e7bb729-a302-4006-adb7-a15853c698f5" />

# VPS Purchase

A VPS (Virtual Private Server) is a virtual machine with its dedicated virtualized CPU, memory, storage, and network resources that is rented to you by a cloud or hosting provider. The name can vary from one supplier to another:  

- AWS called them EC2
- GCP called them compute engine instances
- Azure called them virtual machines
- DigitalOcean called them droplets

As you can see, there are many VPS on the market. For this lab, I rented a VPS on [Namecheap](https://www.namecheap.com/hosting/vps/) with the Pulsar plan. Feel free to choose what you want.  

Here are the steps to buy a VPS on Namecheap:  

**1/ Select your VPS formula**  

<img width="1532" height="997" alt="image" src="https://github.com/user-attachments/assets/934d7bb6-e84e-4e17-a03a-0c5527e4a3ec" />  

<br></br>

Do not select any additional CPU, memory or hard drive space as this will cost you extra fees.  
  
<img width="1422" height="882" alt="image" src="https://github.com/user-attachments/assets/2ed0cf03-b123-4656-a44c-aa10f9001f4a" />  

<br></br>

**2/ Configure your VPS domain name, then add it to your cart**  
  
<img width="1421" height="601" alt="image" src="https://github.com/user-attachments/assets/bbc8c4ec-5e67-480e-853c-775d93ea5caf" />

<br></br>

**3/ Confirm your order**  

Disable the **auto-renew** button when confirming your order, otherwise your subscription will automatically be renewed after its expiration.  

<img width="1362" height="647" alt="image" src="https://github.com/user-attachments/assets/68d8171d-b543-4ac0-85b4-f67a2205553e" />

<br></br>

**4/ Purchase your VPS**

Click on **Pay Now** after reviewing the details of your purchase and agreeing to the Terms of Service:  

<img width="1421" height="601" alt="image" src="https://github.com/user-attachments/assets/36118e98-e746-41e1-bf7b-5bb2ba8ba3d2" />

<br></br>

Going back to your [dashboard](https://ap.www.namecheap.com/dashboard), you should see a server icon next to your domain name:  

<img width="1116" height="117" alt="image" src="https://github.com/user-attachments/assets/b271e60e-4767-4a69-a078-27c07915b942" />

<img width="1427" height="65" alt="image" src="https://github.com/user-attachments/assets/3dced6e7-f97e-40bd-8a7f-e724f39303a9" />  

<br></br>

> Note that the VPS activation takes some time (**generally 15 minutes**). Therefore be patient. Once the VPS activated, you will receive the IP address and credentials in your mailbox.  

<img width="1247" height="786" alt="image" src="https://github.com/user-attachments/assets/76f7ade8-2427-40d9-85fa-94538fcb803d" />

At the bottom of the mail, you will find your SSH credentials as well as the credentials to log in to the VPS admin panel.  

To manage your VPS, click on the `Hosting List` section, then click on `GO TO VPS PANEL`:  

<img width="1432" height="352" alt="image" src="https://github.com/user-attachments/assets/1fa32f1a-bf59-42c3-9fc3-66446e7f1ec9" />

<br></br>

<img width="1187" height="862" alt="image" src="https://github.com/user-attachments/assets/99b5a643-8e9e-417f-9e09-81787ed9f7db" />

## VPS Configuration

Before trying to authenticate to your VPS, it must be online.  

<img width="572" height="272" alt="image" src="https://github.com/user-attachments/assets/ac647d81-64ca-4fd7-ac1b-f265ef01bcb3" />

Once this check done, you can use `ssh` to remotely access your server with the credentials provided in the mail you received:  

```bash
ssh root@<vps_ip_address>
```

<img width="1442" height="807" alt="image" src="https://github.com/user-attachments/assets/ca6e9e35-9ec9-4606-8baa-abd1d922497f" />

One of the first command to execute after connecting to your VPS is:  

```bash
sudo apt update
```

You can then generate an SSH key pair and disable password authentication for security reasons:  

```bash
ssh-keygen -t ed25519 -N '' -f id_ed25519
```

<img width="1282" height="467" alt="image" src="https://github.com/user-attachments/assets/288d4b53-c4e1-4a6b-9c1f-25a60954f8a5" />

Copy your public key in the `.ssh` directory of your root user:  

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@<vps_ip_address>
```

<img width="1515" height="347" alt="image" src="https://github.com/user-attachments/assets/5d6fb494-4409-4818-a11b-6ddae00b4550" />

<img width="1397" height="657" alt="image" src="https://github.com/user-attachments/assets/d01aadad-0a90-4c1c-830a-1aedd33aa602" />

To disable SSH password authentication, use this command:  

```bash
nano /etc/ssh/sshd_config
```

<img width="942" height="96" alt="image" src="https://github.com/user-attachments/assets/1854c31c-5341-4888-b669-45852662ca70" />

```bash
systemctl restart ssh.service
```

# GoPhish

[GoPhish](https://github.com/gophish/gophish) is a phishing toolkit that can be used to quickly and easily setup and execute phishing campaigns.  

## Installation

The fastest way to install GoPhish is via the [release](https://github.com/gophish/gophish/releases/) file.  

```bash
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
```

```bash
apt install -y unzip
unzip ./gophish-v0.12.1-linux-64bit.zip -d gophish
```

<img width="982" height="62" alt="image" src="https://github.com/user-attachments/assets/250bc196-c51c-4b7d-ad21-ed291f6cb604" />


## Configuration

### Firewall Rules

Depending on the VPS you're using, the firewall configuration may differ. If you're using a VPS from Namecheap, follow the next steps, otherwise you can skip this part. That said, make sure that ports tcp/80, tcp/443, and tcp/22 are open on your VPS. Feel free to visit your VPS supplier documentation to learn more about that.  
To configure the firewall rules for a Namcheap VPS, you can use [ufw](https://help.ubuntu.com/community/UFW).  
To check the status of the firewall, use this command:  

```bash
ufw status
```

<img width="815" height="61" alt="image" src="https://github.com/user-attachments/assets/aee3d640-c4cd-4dfb-99cf-2643ccdb0bac" />

As you can see, the firewall is disabled (inactive). To enable it, use this command:  

```bash
ufw enable
```

<img width="1021" height="87" alt="image" src="https://github.com/user-attachments/assets/286b033e-98dd-4989-bfb9-69c22b4dde2e" />

After enabling the firewall, open ports 80, 443, and 22:  

```bash
ufw allow 443
ufw allow 80
ufw allow 22
```

Once done, you can check if the settings were properly applied using this command:  

```bash
ufw status
```

<img width="957" height="292" alt="image" src="https://github.com/user-attachments/assets/5ea36b3e-b914-461c-ad0f-01ae68b2abdb" />

Let's now configure our SMTP relay service.  

### SMTP Relay Service

There are numerous SMTP relay services (Google Workplace, SendGrid, Mailgun, Mailtrap, etc). For this lab, I used [SendGrid](https://www.twilio.com/en-us/sendgrid). Skip the steps below if you used another SMTP relay service.  

To start with SendGrid, you will need to configure the domain name from which your emails will be sent. To do that, go to `Settings > Sender Authentication`, then click on `Authenticate your Domain`:  

<img width="882" height="879" alt="image" src="https://github.com/user-attachments/assets/cb15a912-e505-4e1d-a32e-dc61e485ef98" />

After that, specify your phishing domain name, then click on next:  

<img width="1377" height="500" alt="image" src="https://github.com/user-attachments/assets/e0c98ebb-274b-4fc8-8f73-12b259ac32e2" />

Then, you will need to add the following DNS records to your domain:  

<img width="1667" height="822" alt="image" src="https://github.com/user-attachments/assets/117f1601-0046-473d-8893-ad61fb2db6d3" />

To do that, go back to Namecheap's `Domain List`, then click on `Manage`:  

<img width="1400" height="681" alt="image" src="https://github.com/user-attachments/assets/7989ad29-8b5e-400c-bf57-d8345c40cdbd" />

Next, click on `Advanced DNS`:  

<img width="1358" height="557" alt="image" src="https://github.com/user-attachments/assets/daf41839-c98f-4cb3-a03e-4ba0e140b3b2" />

Finally, go down and click on the `ADD NEW RECORD` button:  

<img width="1104" height="362" alt="image" src="https://github.com/user-attachments/assets/4d1d1cf4-0c02-4bdb-9d60-25214e674350" />

After adding all the records highlighted above, go back to SendGrid and check the box `I've added these records`, then click on Verify:  

<img width="1676" height="821" alt="image" src="https://github.com/user-attachments/assets/e0d49263-f10d-4c99-a751-f81233cc14d7" />

If everything goes as planned, you must see a new column `Status` with the value `Verified`:  

<img width="1878" height="792" alt="image" src="https://github.com/user-attachments/assets/feadd56c-9ca3-41a4-adb1-f5b7afc310b6" />

To get the SMTP server information (user, password, email server, etc.), go to `Email API > Integration Guide`, then select `SMTP Relay`:  

<img width="1587" height="630" alt="image" src="https://github.com/user-attachments/assets/b70febaa-d72e-48a6-acc1-418619311c09" />

<br></br>

<img width="1420" height="767" alt="image" src="https://github.com/user-attachments/assets/20fdc9b6-b0a0-42ac-84d8-bdb915d0f99d" />

As you can see, the server name and username are respectively **smtp.sendgrid.net** and **apikey**. The password is your API key.  

To generate an API key, go to `Settings > API Keys`, then create a new API Key:  

<img width="1797" height="716" alt="image" src="https://github.com/user-attachments/assets/bd07049c-c8ab-4469-8f5d-93e4f80240cb" />

<br></br>

<img width="797" height="362" alt="image" src="https://github.com/user-attachments/assets/c513f5f7-4f5a-47ee-bf7d-1e7ac42b1adc" />

Make sure to copy your API Key in a secure place as you won't be able to retrieve it again.  
Well, let's now configure GoPhish's admin panel server.  

### Admin Panel Server

To configure GoPhish, we are going to edit the `config.json` file located in GoPhish root directory.  

Here is its default content:  

<img width="1212" height="607" alt="image" src="https://github.com/user-attachments/assets/7876a9c7-0b03-458d-a629-288dde222f80" />

To start, change the `listen_url` of your Gophish Admin Server to `0.0.0.0:3333` to listen on all interfaces. To do that, you can use your favorite command line editor, or simply use this command:  

```bash
sed -i 's/127.0.0.1/0.0.0.0/g' config.json
```

<img width="1035" height="192" alt="image" src="https://github.com/user-attachments/assets/64b58c20-206d-484e-9ec8-a91af5db3bdc" />

If you do not want to change the local IP address to `0.0.0.0`, you could use a SSH local port forwarding from your attacker machine:  

```bash
ssh <your_vps_username>@<your_vps_server> -L 127.0.0.1:3333:localhost:3333
```

The command above allows you to access the GoPhish admin login panel from your attacker machine without exposing it on the Internet.  

In this lab, we will restart GoPhish after every change made to the configuration file. As you can guess it, this can quickly become time consuming. To cope with that, we will create a GoPhish service by editing `/etc/systemd/system/gophish.service` with the following content:  

```bash
nano /etc/systemd/system/gophish.service
```

```bash
[Unit]
Description=gophish-service

[Service]
Type=simple
WorkingDirectory=$HOME/gophish/
ExecStart=$HOME/gophish/gophish

[Install]
WantedBy=multi-user.target
```

<img width="972" height="287" alt="image" src="https://github.com/user-attachments/assets/567f895c-6c79-4084-8f99-7e87fb8d81a5" />

> Do not hesitate to change `$HOME/gophish/` if you installed GoPhish in another directory.  

Once done, you can enable your `GoPhish` service using this command:  

```bash
sudo systemctl enable /etc/systemd/system/gophish.service
```

<img width="1487" height="57" alt="image" src="https://github.com/user-attachments/assets/3e3c2fc4-7c95-4fca-a964-023cbd90f923" />

After that, you can start the service with this command:  

```bash
chmod +x $HOME/gophish/gophish
sudo systemctl start gophish
```

Note that, you must give execution permissions to the `gophish` binary before starting the service, otherwise it will fail to start.

<img width="1822" height="602" alt="image" src="https://github.com/user-attachments/assets/036af0ef-e906-4fac-a8a1-fe13ff2bd775" />

To get GoPhish admin panel's password, run the binary:  

```bash
./gophish
```

<img width="1511" height="237" alt="image" src="https://github.com/user-attachments/assets/8cdfb8a4-8602-4481-8063-26b4eca9bde9" />

> By default, GoPhish generates a random password of 16 alphanumerical characters. The default username is `admin`.  

For security reasons, we will configure our firewall to prevent anyone from accessing our GoPhish admin panel. To do that, execute the following command in your Namecheap VPS:  

```bash
sudo ufw allow from <your_public_ip_address> to any port 3333
```

To get your public IP address, run `curl ifconfig.me`.  

To check if the configurations were successfully applied, use this command:  

```bash
ufw status
```

<img width="1067" height="217" alt="image" src="https://github.com/user-attachments/assets/5465fc5f-c712-493c-af35-d3de13465263" />

Let's now access GoPhish admin panel:  

<img width="3020" height="1196" alt="image" src="https://github.com/user-attachments/assets/35ec083e-c4c5-424b-ba36-d98d7e84f0d0" />

After specifying your credentials, you will need to reset your password:  

<img width="955" height="601" alt="image" src="https://github.com/user-attachments/assets/4ba95dd9-bb5b-4390-bcd5-024270579ab5" />

<img width="1222" height="677" alt="image" src="https://github.com/user-attachments/assets/391063bd-6f42-42bf-b7d9-d9700d961150" />

### Phishing Server

In this section, we are going to configure the phishing server that will host our phishing website.  
By default, this port listens on `0.0.0.0:80`. To access it, you will first need to link your phishing domain with your VPS IP address. This can be done by adding an `A` record to your DNS configuration.  

<img width="1102" height="57" alt="image" src="https://github.com/user-attachments/assets/f92882ed-678c-45e0-aeda-3fc79950aeb1" />

> The **@** symbol represents the root (apex) domain. This is a shorthand for the domain itself (phishlab.xyz), not a subdomain.   

To check if the record was successfully added, use this command:  

```bash
nslookup phishlab.xyz
```

<img width="997" height="187" alt="image" src="https://github.com/user-attachments/assets/75e9c972-f637-42b6-aa11-dc6d8748300c" />

As you can see, nslookup resolution worked which means that my record was successfully added.  
After that, you should be able to access your phishing domain:  

<img width="597" height="75" alt="image" src="https://github.com/user-attachments/assets/ad8decd7-a7fa-4bad-b983-0d0a11a13ebb" />

By default, this returns the default 404 page. However, it works!  

Using an HTTP website for a phishing campaign is not a great idea as it may raise suspicion among employees. To increase the chances of our phishing campaign, we'll add a TLS certificate to our phishing website and configure it to listen on port 443.  

### TLS Certificate

By default, your phishing server listens on port 80, which may trigger warnings in the target's browser.  

<img width="596" height="57" alt="image" src="https://github.com/user-attachments/assets/58dc99ac-9e2a-4869-9f0f-d3b12fe1f720" />

To deal with that, let's first install [certbot](https://certbot.eff.org/pages/about):  

```bash
sudo apt install -y certbot
```

<img width="1787" height="420" alt="image" src="https://github.com/user-attachments/assets/7f312f52-d78f-4344-a902-a9cb782ed85f" />

To generate a new `Let’s Encrypt` certificate, use this command:  

```bash
certbot certonly -d '<your_phishing_domain_name>' --manual --preferred-challenges dns --register-unsafely-without-email
```

<img width="1708" height="780" alt="image" src="https://github.com/user-attachments/assets/84061d8a-6c39-474e-8ee8-823e2ad48c26" />  

Then, add the `_acme-challenge` TXT record to your DNS configuration.  

<img width="1097" height="51" alt="image" src="https://github.com/user-attachments/assets/8f84be05-0d08-498a-a042-24e7bac4e403" />

Once done, you can use [Google Admin Toolbox](https://toolbox.googleapps.com/apps/dig/#TXT/) to check if the record was successfully added:  

<img width="1527" height="691" alt="image" src="https://github.com/user-attachments/assets/59f1fb5c-2f7f-4bf0-a70d-b3586f1aab1f" />

After that, go back to `certbot` command line, and press `[ENTER]` to continue.  

<img width="1841" height="420" alt="image" src="https://github.com/user-attachments/assets/1079c81a-f766-4a6b-b2b2-aa4ceb84d6c0" />

If everything goes as planned, `certbot` will generate a certificate with its corresponding private key in the `/etc/letsencrypt/live/` directory.  

Then, you can update your `config.json` file by making the following changes:  

- Change `listen_url` to 0.0.0.0:443
- Change `use_tls` to `true`
- Change `cert_path` with the certificate (.pem) generated by certbot
- Change `key_path` with the private key (.pem) generated by certbot

<img width="1587" height="602" alt="image" src="https://github.com/user-attachments/assets/2692e3c4-5e87-445f-b4c4-7952ffcbd902" />

Once done, you should now be able to access your phishing website using HTTPS:  

<img width="1222" height="582" alt="image" src="https://github.com/user-attachments/assets/d6453d3a-3c90-413e-8a55-379ba88d0741" />

Let's now start our first phishing campaign. Shall we?  

### Sending Profiles

**[Sending Profiles](https://docs.getgophish.com/user-guide/documentation/sending-profiles)** is a GoPhish feature that allows you to configure your SMTP relay service. This is where you will specify your SMTP server, username and password, as well as the email address that will be used to send emails to your targets.  

To create a new sending profile, click on the `Sending Profiles` section:  

<img width="3002" height="696" alt="image" src="https://github.com/user-attachments/assets/3bd93ddc-d7a5-4f94-87a1-f4bdb53a0a8d" />

Before creating your profile, you will need to verify that you own the email address that will be used by GoPhish for sending phishing emails to your targets.  

If you used SendGrid as a SMTP relay service, go to `Settings > Sender Authentication > Single Sender Verification`:  

<img width="877" height="873" alt="image" src="https://github.com/user-attachments/assets/f67fe0d5-53d9-466f-9a83-469e6941aaa4" />

After clicking on `Verify a Single Sender`, click on `Create New Sender`:  

<img width="1678" height="110" alt="image" src="https://github.com/user-attachments/assets/f2139249-a1a5-412f-9460-8cdde36fc5b9" />

Then, fill out the fields with your information:  

<img width="1622" height="713" alt="image" src="https://github.com/user-attachments/assets/4b294336-8326-484c-b0c7-710ebcc8f8d3" />

If everything goes as planned, you must see a new entry in the `Single Sender Verification` section:  

<img width="1678" height="257" alt="image" src="https://github.com/user-attachments/assets/78293eaa-448c-4ecc-8326-c97c33d5759a" />

The overall configuration must look like this:  

<img width="1451" height="805" alt="image" src="https://github.com/user-attachments/assets/605bb505-782d-4e56-b725-45188d561b82" />

Once the `Single Sender Verification` configuration done, proceed by adding a new sending profile in GoPhish.  

To do that, complete your sending profile with these information:  

- The host is `smtp.sendgrid.net:587`
- Username is **apikey**
- Password is the API key you generated in the `Settings > API Keys` section
- SMTP From is the email address you configured in the `Single Sender Verification`

> Note that this only works for SendGrid SMTP relay service. For instance, Gmail SMTP relay service configuration will look like [this](https://youtu.be/8Q6EtC8jzpM?si=zNWM14EOkdW7yYgb&t=74).

<img width="1296" height="990" alt="image" src="https://github.com/user-attachments/assets/8435d74f-85e6-462a-a727-aedfb783c358" />

To test your sending profile configuration, you can click on `Send Test Email`. This will try to send an email to a target email address of your choice using the SMTP relay service you configured in the `Sending Profile` section.  

To generate a temporary email, you can use [temp-mail](https://temp-mail.org/).  

<img width="576" height="252" alt="image" src="https://github.com/user-attachments/assets/3b5cc7c9-90c7-46ff-8a89-d7c648592a23" />

After generating your temporary email, click on `Send Test Email`, then fill out the fields and click on Send` to send your test email.  

<img width="1302" height="992" alt="image" src="https://github.com/user-attachments/assets/3661e16e-7c1e-4923-93e5-9c6226adf72f" />

You should normally see this message:  

<img width="687" height="312" alt="image" src="https://github.com/user-attachments/assets/4b03c0c5-61ca-4172-8341-56c0459a6914" />

When taking a look to your temporary email's inbox, you should receive an email:  

<img width="720" height="191" alt="image" src="https://github.com/user-attachments/assets/6e812df5-16b2-464b-b408-e9abaee3d111" />

<img width="717" height="331" alt="image" src="https://github.com/user-attachments/assets/900e5de9-113a-4457-b4cd-5798ed9e5068" />

Finally save your changes to avoid losing them.

### Email Templates

**[Email templates](https://docs.getgophish.com/user-guide/documentation/templates)** is the content of the email that is sent to your targets. This is what your targets will read.  

<img width="1300" height="992" alt="image" src="https://github.com/user-attachments/assets/57daa62d-a3ab-405a-ba4b-7e82ea76c925" />

In this section, you will need to provide these information:  

- The sender email address
- The subject of the email
- The body or email template

Regarding the email template, you can use the template below. This is the default email sent by [Wordpress.org](https://wordpress.org/) after a user creates an account.  

```html
<html>
<head>
	<title></title>
</head>
<body>
  <p>Hi {{.FirstName}},</p>
  <p>Welcome to WordPress.org! Your new account has been setup.</p>
  <p>Your username is: {{.FirstName}}<br />
  You can create check the features and discounts at the following URL:<br />
  <a href="{{.URL}}">https://discount.wordpress.org/5c31730639f0b6966d872d6895a4810c/</a></p>
  
  <p>-- The WordPress.org Team</p>
{{.Tracker}}</body>
</html>
```

`{{.FirstName}}`, `{{.URL}}`, and `{{.Tracker}}` are variables that will be automatically replaced by GoPhish when you send your emails. To learn more about them, refer [here](https://docs.getgophish.com/user-guide/template-reference).

Note that you can import an email's source code using the `Import Email` button.  

As usual, make sure to save your template to not lose your modifications.  

<img width="680" height="67" alt="image" src="https://github.com/user-attachments/assets/d3fe03f0-347f-4cf0-adc1-22fb7ad86da0" />

### Landing Pages

**[Landing Pages](https://docs.getgophish.com/user-guide/documentation/landing-pages)** are the phishing page that you will use to trick your targets. GoPhish has a feature called `Import Site` that allows you to clone a webpage.  

Let's try to clone [Wordpress.org's login page](https://login.wordpress.org/).  

To do that, click on the `Import Site` button on the `Landing Pages` section:  

<img width="1307" height="763" alt="image" src="https://github.com/user-attachments/assets/48f86799-c78e-4f9e-a4fc-04894d29aa04" />

<br></br>

<img width="686" height="263" alt="image" src="https://github.com/user-attachments/assets/73a34d0f-9686-4de3-a244-d3070f1c333e" />

<br></br>

<img width="1297" height="993" alt="image" src="https://github.com/user-attachments/assets/0b9e84e2-4513-4e8b-911b-94a3a3aaf31b" />

As you can see the page was successfully cloned. To capture credentials, check the "Capture Submitted Data" and "Capture Passwords" boxes. Furthermore, to avoid raising any suspicion, you can redirect the target to a website of your choice:  

<img width="677" height="178" alt="image" src="https://github.com/user-attachments/assets/ea9b2abc-1cc9-44e7-bac7-d8a7c4a5e6ea" />

After that, save your landing page configuration.  

### Users & Groups

**[Users & Groups](https://docs.getgophish.com/user-guide/documentation/groups)** section is used to specify the target users to which your email will be sent. These users will be placed in various groups depending on their roles, permissions, etc. For instance, the email you will send to executives will not be the same as the email you will send to HR.  

<img width="1301" height="600" alt="image" src="https://github.com/user-attachments/assets/072bfe65-6608-4aa5-bf69-f7effde7221b" />

Note that, you can also add users by importing them using a `.csv` file.  

Once done, click on save.  

<img width="1325" height="437" alt="image" src="https://github.com/user-attachments/assets/09ace366-7608-4fc5-a21e-fdddcc9c4544" />


### Campaigns

**[Campaigns](https://docs.getgophish.com/user-guide/documentation/campaigns)** is a feature that is used for sending emails to one or more groups and monitoring for opened emails, clicked links, or submitted credentials.  

To launch your campaign, click on the `Campaigns` section:  

<img width="1303" height="788" alt="image" src="https://github.com/user-attachments/assets/952ffdb5-bdb6-4daa-a137-06847bdb7713" />

Make sure to replace the `URL` section with your phishing website URL.  

Before starting your phishing campaign, you can test if everything works properly by clicking on `Send Test Email`. Beware to not send your test email to your real targets. Use instead a [temporary email](https://temp-mail.org/).  

After that, launch your campaign by clicking on the `Launch Campaign` button:  

<img width="1305" height="788" alt="image" src="https://github.com/user-attachments/assets/5ebe91c9-c96d-4e61-aac7-9fa7d1eb7ce7" />

You should see a dashboard similar to this one:  

<img width="1582" height="876" alt="image" src="https://github.com/user-attachments/assets/e1577a6d-9ce2-4411-bc75-88d514e1f1ce" />

When taking a look at the target's mailbox, we can see that they receive our phishing email:  

<img width="713" height="57" alt="image" src="https://github.com/user-attachments/assets/5bef65a3-9950-45c3-ab69-e584e56fcc94" />

Here is the content of the email:  

<img width="700" height="276" alt="image" src="https://github.com/user-attachments/assets/29f30572-6113-47e2-a48d-1d6cc6c26206" />

Let's try to click on the phishing link:  

<img width="1587" height="813" alt="image" src="https://github.com/user-attachments/assets/d7df86d3-427b-485e-a91f-7d8252e37502" />

We are redirected to the phishing website specified in the `Landing Pages` section.  

When taking a look at the `Campaigns` section, you can see that GoPhish highlighted that the target opened the email address and clicked on the link.  

<img width="1566" height="815" alt="image" src="https://github.com/user-attachments/assets/61696f7b-e652-48ad-ad41-67ff46fde00a" />

Let's now try to enter some credentials:  

<img width="1583" height="809" alt="image" src="https://github.com/user-attachments/assets/e7aa74f7-8356-4303-8f9b-8691d32d9cf6" />

This redirected us to `https://login.wordpress.org` which is the URL we configured in the `Landing Pages` section.  

<img width="1592" height="819" alt="image" src="https://github.com/user-attachments/assets/3d1c8ea2-7cbb-4bee-a5d6-4153ef816705" />

When visualizing our GoPhish campaign dashboard, we can see that the target submitted data:  

<img width="1576" height="812" alt="image" src="https://github.com/user-attachments/assets/0fa49a29-bfc3-4435-96cf-02b7cd04b69b" />

<img width="1565" height="1015" alt="image" src="https://github.com/user-attachments/assets/f5f5e63f-c834-4ac0-9cb1-357cd8db97cb" />

As you can see, GoPhish intercepted the username and password of the target. Using that, we can attempt to authenticate to their account.  


# Evilginx Community

[Evilginx](https://github.com/kgretzky/evilginx2) is a Man-in-The-Middle attack framework used for phishing login credentials along with session cookies. Instead of sending victims to a fake cloned website, it sits between the user and the real website, allowing attackers to perform session hijacking and bypass MFA. Indeed with a session cookie, you won't need to know a target's OTP (One Time Password) to access their account.  
Let's now see how to install and configure Evilginx.

## Installation and Configuration

Evilginx can be installed from its sources or via its pre-compiled binary. Follow the steps below to install it from source:  

```bash
git clone https://github.com/kgretzky/evilginx2
```

```bash
apt install -y golang-go
```

```bash
go build
```

> Do not interrupt the build, as it may take a few seconds to complete.  

<img width="1507" height="82" alt="image" src="https://github.com/user-attachments/assets/5b309899-8928-4e2e-bda7-c56c7f6a0b22" />  

To install Evilginx using its [binary](https://github.com/kgretzky/evilginx2/releases/latest), follow these steps:  

```bash
wget https://github.com/kgretzky/evilginx2/releases/download/v3.3.0/evilginx-v3.3.0-linux-64bit.zip
```

<img width="1552" height="52" alt="image" src="https://github.com/user-attachments/assets/049162f8-b85a-48e3-91b3-d1ae9accb365" />

```bash
unzip evilginx-v3.3.0-linux-64bit.zip -d evilginx
```

<img width="1127" height="207" alt="image" src="https://github.com/user-attachments/assets/e448838c-6a01-4513-91d2-2a54569c42f1" />

After that, give `evilginx` execution permissions:  

```bash
chmod +x ./evilginx
```

<img width="977" height="80" alt="image" src="https://github.com/user-attachments/assets/1a813f51-2492-4f03-a73e-9da4ebe8b90d" />

Once done, launch `evilginx`:  

```bash
./evilginx
```

<img width="1674" height="951" alt="image" src="https://github.com/user-attachments/assets/2b3c7463-f584-4cdf-863a-9c05fc9e6788" />

As you can see, Evilginx failed to start a DNS server on `port 53`. This occured because the port is being used by another process on the system. To check it, use this command:  

```bash
sudo lsof -i :53
```

<img width="1211" height="157" alt="image" src="https://github.com/user-attachments/assets/a7e19dae-8622-4e65-8d0e-3fb86e48e936" />  

To deal with that, you will first need to stop the `systemd-resolved` service, then remove the `/etc/resolv.conf` file:  

```bash
sudo systemctl stop systemd-resolved.service
```

```bash
lsof -i :53
```

<img width="877" height="52" alt="image" src="https://github.com/user-attachments/assets/cc2d4eac-0cfc-4778-9853-a24108c127f3" />

```bash
mv /etc/resolv.conf /etc/resolv.conf.bak
```

<img width="901" height="30" alt="image" src="https://github.com/user-attachments/assets/bc3cc72c-e756-4e22-bd89-37928e53b8fe" />

After that, execute the following command to create a new `/etc/resolv.conf` with your favorite recursive DNS servers:  

```bash
echo -e 'nameserver 1.1.1.1\nnameserver 9.9.9.9' >> /etc/resolv.conf
```

<img width="982" height="82" alt="image" src="https://github.com/user-attachments/assets/d2e9343c-6f93-4ef2-96d7-438bc993188d" />

To check if the DNS resolution works, you can perform an `nslookup`:  

```bash
nslookup google.com
```

<img width="1455" height="657" alt="image" src="https://github.com/user-attachments/assets/9aaa4e61-de1d-46da-b5e2-96dce45bcf61" />

See that Evilginx uses port `tcp/443` to host your phishing website, you will need to reconfigure your GoPhish's phishing server URL to listen on another port (eg: tcp/8843).  

<img width="1422" height="602" alt="image" src="https://github.com/user-attachments/assets/d1bbd7fc-db97-4e73-8487-e5aab01f3b91" />

After that, restart your Gophish service to apply the changes:  

```bash
systemctl restart gophish
```

```bash
systemctl status gophish
```

<img width="1671" height="255" alt="image" src="https://github.com/user-attachments/assets/a34a86eb-4fb5-4a9d-ab46-4702a3b76e0f" />

Let's now configure the domain, and the external IPv4 address:  

```
config domain <your_phishing_domain_name>
```

<img width="977" height="57" alt="image" src="https://github.com/user-attachments/assets/0130017a-7c4a-42f4-b52f-5b16d658214c" />

```
config ipv4 external <your_phishing_domain_ipv4_address>
```

<img width="792" height="52" alt="image" src="https://github.com/user-attachments/assets/64bfc46d-c386-4d52-a49e-c561b3adbe63" />

Enter the `Help` command to get some help:  

<img width="1242" height="325" alt="image" src="https://github.com/user-attachments/assets/02e8019d-3bef-4220-9bf0-c1d59dd149d6" />

In the next section, we will learn how to configure phishlets.  

## Phishlets

[Phishlets](https://help.evilginx.com/community/guides/phishlets) are small yaml configuration files, used to configure Evilginx for targeting specific websites. By default, they are stored under the `phishlets` directory.  

```bash
cd phishlets/
```

```bash
cat example.yaml
```

<img width="1906" height="647" alt="image" src="https://github.com/user-attachments/assets/6aaac44b-8516-4743-8ad4-6a51cb06446a" />

Refer to the command below to download more phishlets [here](https://github.com/An0nUD4Y/Evilginx-Phishlets).  

```bash
git clone https://github.com/An0nUD4Y/Evilginx-Phishlets.git
```

<img width="1287" height="211" alt="image" src="https://github.com/user-attachments/assets/3a2976ad-646a-456a-9dcc-20f5dab2cb40" />

> Note that you can also create your own [phishlets](https://help.evilginx.com/pro/phishlets/) if you want to.  

<img width="1825" height="497" alt="image" src="https://github.com/user-attachments/assets/dd728522-d13c-49d2-a439-8bc37edd1125" />

Let's use the `wordpress.org.yaml` phishlet to better understand the structure of a phishlet:  

<img width="1616" height="982" alt="image" src="https://github.com/user-attachments/assets/4693a436-9c6a-4c32-9071-9509a3c92454" />

<img width="1082" height="357" alt="image" src="https://github.com/user-attachments/assets/f54e6a9a-e125-4586-9702-8ce6e3aea6b2" />

Here is a quick explanation of the different fields in the yaml file:  

- min_ver: This is the minimal version of Evilginx used by the phishlet
- proxy_hosts: Defines which subdomains to proxy to Evilginx
- auth_tokens: Represent the session tokens we want to steal
- credentials: Represent the credentials we want to capture

Note that the option `is_landing: true` tells Evilginx that this host is where victims are expected to first arrive.  

After that, add the highlighted subdomains (login, make, profiles) above to your phishing domain's DNS records as A records:  

<img width="1377" height="217" alt="image" src="https://github.com/user-attachments/assets/2f34e7ba-54e6-4611-b57f-0c73524e8f4a" />

Make sure, your phishlet is located in the `phishlets` directory, otherwise it won't be found by Evilginx:  

<img width="777" height="52" alt="image" src="https://github.com/user-attachments/assets/fe934d8b-ba02-4b1d-b82e-a275b1854e22" />

Once done, re-execute `evilginx`:  

```bash
./evilginx
```

<img width="1636" height="770" alt="image" src="https://github.com/user-attachments/assets/f5cece78-402e-4a8f-981e-dee941945ef3" />

To better understand how to use the `phishlets`, use this command:  

```
help phishlets
```

<img width="1777" height="772" alt="image" src="https://github.com/user-attachments/assets/fce8b1ce-40a3-4206-9ee5-7c0be580e2e5" />

To hide the **example** phishlet, use this command:  

```
phishlets hide example
```

<img width="1202" height="62" alt="image" src="https://github.com/user-attachments/assets/1031678a-43c2-40fe-802a-bfac3e72d76a" />

To enable `wordpress.org` phishlet and request an SSL/TLS certificate, use the following command:  

```
phishlets enable wordpress.org
```

<img width="1257" height="81" alt="image" src="https://github.com/user-attachments/assets/79142bb6-aafe-4d88-bfd7-fae542c9b83a" />

This returned an error stating that `wordpress.org` phishlet requires its hostname to be set up.  

To fix that, use this command:  

```
phishlets hostname wordpress.org <your_phishing_domain>
```

<img width="1005" height="53" alt="image" src="https://github.com/user-attachments/assets/df9fbde4-d887-4d81-9559-c05c29294513" />

<img width="1122" height="210" alt="image" src="https://github.com/user-attachments/assets/28729bfa-9d32-4c9d-9ab7-d85b23027f1d" />

After that, enable the phishlet:  

```
phishlets enable wordpress.org
```

<img width="1907" height="445" alt="image" src="https://github.com/user-attachments/assets/b28882a2-3fea-49bf-889a-ccc08fcbb6ee" />

<img width="1157" height="205" alt="image" src="https://github.com/user-attachments/assets/b69b89ad-e281-4437-9cc2-f516c8f90f4d" />

In my case, it worked. However, you may come across this error when enabling your phishlet:

<img width="1907" height="306" alt="image" src="https://github.com/user-attachments/assets/9611256c-1346-4315-8a9d-b751a6d5251d" />

To fix that, you will need to add the `_acme_challenge` TXT record with the value returned by Evilginx.  

<img width="947" height="52" alt="image" src="https://github.com/user-attachments/assets/3592da3e-5479-4c27-ba02-ee2162ec9f3a" />

<img width="1832" height="807" alt="image" src="https://github.com/user-attachments/assets/a22eca23-4fa0-4dad-9e31-c92110579fb0" />

<img width="1257" height="207" alt="image" src="https://github.com/user-attachments/assets/b707755c-3860-4172-8ec9-98a043211430" />

Here is a little trick to disable log output for blacklist messages:  

```bash
blacklist log off
```

<img width="1042" height="72" alt="image" src="https://github.com/user-attachments/assets/fcfe63a6-63b4-4722-8d20-43881558d682" />

This tells Evilginx to stop showing warnings regarding blacklisted IP addresses.  
Let's now generate our phishing link using lures.  

## Lures

[Lures](https://help.evilginx.com/community/guides/lures) are pre-generated phishing links, that you will send to your targets.  

```
help lures
```

<img width="1510" height="720" alt="image" src="https://github.com/user-attachments/assets/c04740cc-9663-4663-9a3b-2e03c032cf95" />

To create a lure for your `wordpress.org` phishlet, use this command:  

```
lures create wordpress.org
```

<img width="875" height="59" alt="image" src="https://github.com/user-attachments/assets/3b239295-7fe7-4ebe-affb-d7038908a0d8" />

<img width="1361" height="242" alt="image" src="https://github.com/user-attachments/assets/63e57e1b-d803-49fe-ae9b-c61e0be84c99" />

To get the lure's URL, use this command:  

```
lures get-url 0
```

<img width="867" height="84" alt="image" src="https://github.com/user-attachments/assets/d0e4c1e3-30fc-4b83-a2c4-75c1ed73f3dd" />

This is the link you will send to your targets.  

To display all lures, run this command:

```bash
lures
```

<img width="1287" height="180" alt="image" src="https://github.com/user-attachments/assets/266a4d16-3e68-482a-b7bf-a4c6ee9e2c0d" />

> Note that IP addresses will automatically be blacklisted by Evilginx when a user tries to access your phishing website without specifying the lure. This prevents unauthorized access and make detection harder.  

## Sessions

[Sessions](https://help.evilginx.com/community/guides/sessions) represent an history of users who cliked on your lures. Sessions also record credentials and captured session cookies.  

To start, let's copy our lure's URL and open it in our browser:    

<img width="1757" height="987" alt="image" src="https://github.com/user-attachments/assets/c7605a53-f4ef-483d-a1f1-d34bc3441821" />

As you can see, I landed on a Wordpress login page.  

Let's now try to enter some credentials on your Wordpress phishing website:  

<img width="862" height="777" alt="image" src="https://github.com/user-attachments/assets/f6885246-7cc4-4486-afbf-eee2ec3159f2" />

To check if Evilginx captured the credentials, use this command:  

```
sessions
```

For some reasons, it didn't work for me, but it must normally work in your scenario.   

# GoPhish x Evilginx

In this section, we will quickly see how to combine Evilginx and GoPhish.  

One of the main differences between GoPhish and Evilginx is that GoPhish is a **phishing campaign management platform**, whereas Evilginx is a **reverse-proxy framework** that does not provide built-in campaign management features like GoPhish. Additionally, Evilginx is commonly used in assessments to evaluate authentication flows involving multi-factor authentication.  

To combine GoPhish and Evilginx, create a new campaign and replace the `URL` section in GoPhish `Campaigns` with your Evilginx's lure URL, then launch your campaign.  
Here is my lure:  

<img width="956" height="80" alt="image" src="https://github.com/user-attachments/assets/b81f14fa-abb6-4cb8-a5db-91ace2b4300b" />

Replacing it gave me something like this:  

<img width="1392" height="1037" alt="image" src="https://github.com/user-attachments/assets/5e4a0608-5b43-4b88-896b-6f0565a2ab56" />

Once done, I save my settings and launch the campaign.  

When taking a look at the Campaign dashboard, we can see that the email was successfully sent.  

<img width="1537" height="1005" alt="image" src="https://github.com/user-attachments/assets/085d9168-18d9-400a-9d30-da2384cb37cf" />

To verify that we can check the target's email inbox:  

<img width="896" height="362" alt="image" src="https://github.com/user-attachments/assets/7b8ac322-6356-43db-99d2-d326137767f9" />

Let's click on the link in the email:  

<img width="1387" height="947" alt="image" src="https://github.com/user-attachments/assets/9d9dc9ee-df2c-4fec-9ba8-3feb4b3fe1a1" />

As you can notice, Evilginx captures the target's session. 

<img width="1282" height="190" alt="image" src="https://github.com/user-attachments/assets/227de8bb-2265-4c1a-969f-625dde8a6ac2" />

If you're curious to learn more about how to combine Evilginx and GoPhish, refer to [Evilgophish](https://github.com/fin3ss3g0d/evilgophish).  

# Pitfalls to avoid during a phishing campaign

- Replace generic greetings such as "Dear Customer" with personalized messages.
- Fix grammatical and spelling mistakes, as they can raise suspicion.
- Use high-quality images instead of low-resolution ones.
- Avoid suspicious sender email addresses, such as Gmail addresses.
- Replace random phishing URLs with custom, realistic URLs.

# Tips and Tricks

- Subscribe to the company's newsletter to identify their email naming convention and upcoming events that you can use as a pretext during our phishing campaign.
- Use [mailtrap.io](https://mailtrap.io/) to test your phishing emails before sending them to your victims.
- Check everything before launching your phishing campaign. Ensure your phishing tool captures credentials and session cookies correctly, and verify that it displays properly your phishing website across different browsers.
- Close the loop. For example, redirect users to the legitimate website after capturing their credentials so they are less likely to realize they have been phished.
- By default, Evilginx wEvilginx blocks IP addresses that access the server without a valid lure. If this happens, you will be redirected to [rickroll](https://www.youtube.com/watch?v=dQw4w9WgXcQ) video. To fix that, remove your IP address from `/root/.evilginx/blacklist.txt`

# Resources

- [A Technical Deep Dive into Modern Phishing Methodologies](https://blog.quarkslab.com/technical-dive-into-modern-phishing.html)
- [Phishing Campaign: Objectives, Methodology](https://www.vaadata.com/en/blog/phishing-campaign-objectives-methodology-spear-and-mass-phishing-examples/)
- [Practical phishing campaign | TCM Security](https://www.youtube.com/watch?v=xWLeTdKvC3Y)
- [OPSEC on the High Seas: A Gophish Adventure](https://www.youtube.com/watch?v=QG93uvylpoM)
- [BHIS | How to Build a Phishing Engagement](https://www.youtube.com/watch?v=VglCgoIjztE)
- [Evilginx-Phishing-Infra-Setup](https://github.com/An0nUD4Y/Evilginx-Phishing-Infra-Setup)
- [Using the SMTP Relay Feature with SendGrid](https://support.nimbushosting.co.uk/docs/using-the-smtp-relay-feature-with-sendgrid)
- [Domain Verification Setup Guide](https://help.mailgun.com/hc/en-us/articles/32884702360603-Domain-Verification-Setup-Guide)
- [GoPhish Documentation](https://docs.getgophish.com/user-guide)
- [Evilginx Documentation](https://help.evilginx.com/community)
- [Evilginx Reddit Feed](https://www.reddit.com/r/redteamsec/comments/183nejy/evilgophish_lures/)


# Disclaimer

This lab is intended solely for educational purposes and authorized security testing. Do not use its contents against systems or individuals without explicit permission. The authors are not responsible for any misuse or damage resulting from the use of this repository.
