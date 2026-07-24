<img width="1676" height="821" alt="image" src="https://github.com/user-attachments/assets/b4f5a0b3-631e-4528-aee7-a019245f173a" /># Context

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

<img width="1060" height="749" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/621289226-94e2492f-652c-4757-ab46-09ac11865f3c.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011142Z&X-Amz-Expires=300&X-Amz-Signature=c3479d0f7bea294a1c94be91157602893ef9d9c8a6a7d3eb3db9ed660fdc3f9e&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />

Depending on your budget, add a domain name to your cart, then follow the next instructions.  

**2/ Confirm the order**  

Before confirming your order, make sure you disable the **auto-renew** option for your domain. If enabled, this will automatically renew your subscription. Once done, click on `Confirm Order`.  

<img width="1356" height="647" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/621287108-99295cc6-0753-4bbd-9a3b-ef8480cc0308.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011429Z&X-Amz-Expires=300&X-Amz-Signature=b0397563dc2757098ee88948fb7697149bc0aa6eb48aedbf78cedea6b9e687f1&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />

<br></br>

**3/ Enter your credit card information and purchase your domain**  

The final step consists of purchasing your domain name after entering your credit card information.  
Moreover do not select any additional options if not required. Once done, click on `Continue`.  

<img width="1341" height="636" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/621287825-e082ae3b-2aa3-430a-a2c6-77d3929a7ef9.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011445Z&X-Amz-Expires=300&X-Amz-Signature=70a848090fc84030e116f164776d50c3ec353b4ea0bab73f95880dd34bb70aca&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />

<br></br>

**4/ Access your purchased domain**  

Here is how to access your domain:  

<img width="1372" height="496" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/621283869-7e7bb729-a302-4006-adb7-a15853c698f5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011537Z&X-Amz-Expires=300&X-Amz-Signature=bb76e74cfe91917a7e65e7225a3c1d7472c74e93efdd1850b7ac166f88153fef&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />

# VPS Purchase

A VPS (Virtual Private Server) is a virtual machine with its dedicated virtualized CPU, memory, storage, and network resources that is rented to you by a cloud or hosting provider. The name can vary from one supplier to another:  

- AWS called them EC2
- GCP called them compute engine instances
- Azure called them virtual machines
- DigitalOcean called them droplets

As you can see, there are many VPS on the market. For this lab, I rented a VPS on [Namecheap](https://www.namecheap.com/hosting/vps/) with the Pulsar plan. Feel free to choose what you want.  

Here are the steps to buy a VPS on Namecheap:  

**1/ Select your VPS formula**  

<img width="1532" height="997" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/621305674-934d7bb6-e84e-4e17-a03a-0c5527e4a3ec.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011555Z&X-Amz-Expires=300&X-Amz-Signature=4c95fbb201645efafd9ff309be009c426e669628e720d1ca9218a6a0fadecfac&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />  

<br></br>

Do not select any additional CPU, memory or hard drive space as this will cost you extra fees.  
  
<img width="1422" height="882" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/620304926-2ed0cf03-b123-4656-a44c-aa10f9001f4a.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011611Z&X-Amz-Expires=300&X-Amz-Signature=980d100c2420c36db8b01cd17ac3c0d3e02a3a0152a4d0fdff4b45e56a791a0d&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />  

<br></br>

**2/ Configure your VPS domain name, then add it to your cart**  
  
<img width="1421" height="601" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/625137289-bbc8c4ec-5e67-480e-853c-775d93ea5caf.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011627Z&X-Amz-Expires=300&X-Amz-Signature=f3b84d4104bcda4b0a69374c92e20e0b9bed2bb4dd141a8f1aaa379eb509027c&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />

<br></br>

**3/ Confirm your order**  

Disable the **auto-renew** button when confirming your order, otherwise your subscription will automatically be renewed after its expiration.  

<img width="1362" height="647" alt="image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/64969369/625134364-68d8171d-b543-4ac0-85b4-f67a2205553e.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260724%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260724T011645Z&X-Amz-Expires=300&X-Amz-Signature=bc2a73f3c6fbdfcc2af932f89499eb9cb0b69ae6bb41dfc29724eebea9776b04&X-Amz-SignedHeaders=host&response-content-type=image%2Fpng" />

<br></br>

**4/ Purchase your VPS**

Click on **Pay Now** after reviewing the details of your purchase and agreeing to the Terms of Service:  

<img width="1421" height="601" alt="image" src="https://github.com/user-attachments/assets/5891cc18-23e6-4055-9534-c6ba55ef3e1a" />

<br></br>

Going back to your [dashboard](https://ap.www.namecheap.com/dashboard), you should see a server icon next to your domain name:  

<img width="1116" height="117" alt="image" src="https://github.com/user-attachments/assets/6940ad1a-5e82-4d76-afac-73a6c5958dba" />

<img width="1427" height="65" alt="image" src="https://github.com/user-attachments/assets/3dced6e7-f97e-40bd-8a7f-e724f39303a9" />  

<br></br>

> Note that the VPS activation takes some time (**generally 15 minutes**). Therefore be patient. Once the VPS activated, you will receive the IP address and credentials in your mailbox.  

<img width="1247" height="786" alt="image" src="https://github.com/user-attachments/assets/7f98e470-1fe1-4188-91d7-a212d2c006ad" />

At the bottom of the mail, you will find your SSH credentials as well as the credentials to log in to the VPS admin panel.  

To manage your VPS, click on the `Hosting List` section, then click on `GO TO VPS PANEL`:  

<img width="1432" height="352" alt="image" src="https://github.com/user-attachments/assets/b1290754-1260-4cf9-a82f-98a9a18f3c14" />

<br></br>

<img width="1187" height="862" alt="image" src="https://github.com/user-attachments/assets/9a743454-29c5-45b9-9e05-69580fb9cf9e" />

## VPS Configuration

Before trying to authenticate to your VPS, it must be online.  

<img width="572" height="272" alt="image" src="https://github.com/user-attachments/assets/7e3ae664-2b1e-4351-9edd-6822f01ce59f" />

Once this check done, you can use `ssh` to remotely access your server with the credentials provided in the mail you received:  

```bash
ssh root@<vps_ip_address>
```

<img width="1442" height="807" alt="image" src="https://github.com/user-attachments/assets/e563f583-39b5-47c4-907f-ae329b0a2696" />

One of the first command to execute after connecting to your VPS is:  

```bash
sudo apt update
```

You can then generate an SSH key pair and disable password authentication for security reasons:  

```bash
ssh-keygen -t ed25519 -N '' -f id_ed25519
```

<img width="1282" height="467" alt="image" src="https://github.com/user-attachments/assets/6a0b477f-5de5-4c5b-9241-fe780b43733b" />

Copy your public key in the `.ssh` directory of your root user:  

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@<vps_ip_address>
```

<img width="1515" height="347" alt="image" src="https://github.com/user-attachments/assets/a49d60f5-e749-4aec-b4ef-e5b59b8ecd17" />

<img width="1397" height="657" alt="image" src="https://github.com/user-attachments/assets/b4c06cb6-81b1-4849-b742-fa74bfe62d94" />


To disable SSH password authentication, use this command:  

```bash
nano /etc/ssh/sshd_config
```

<img width="942" height="96" alt="image" src="https://github.com/user-attachments/assets/7a8af0ea-a560-4cb3-af18-b24a117f4ff0" />

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

<img width="982" height="62" alt="image" src="https://github.com/user-attachments/assets/2b71f13f-e5e6-4adb-8158-c8e03129470c" />


## Configuration

### Firewall Rules

Depending on the VPS you're using, the firewall configuration may differ. If you're using a VPS from Namecheap, follow the next steps, otherwise you can skip this part. That said, make sure that ports tcp/80, tcp/443, and tcp/22 are open on your VPS. Feel free to visit your VPS supplier documentation to learn more about that.  
To configure the firewall rules for a Namcheap VPS, you can use [ufw](https://help.ubuntu.com/community/UFW).  
To check the status of the firewall, use this command:  

```bash
ufw status
```

<img width="815" height="61" alt="image" src="https://github.com/user-attachments/assets/8ad5fd06-a51c-42ad-84dd-8a24f712f428" />

As you can see, the firewall is disabled (inactive). To enable it, use this command:  

```bash
ufw enable
```

<img width="1021" height="87" alt="image" src="https://github.com/user-attachments/assets/393c0cff-c252-4fb1-8f25-7bccb5f358a2" />

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

<img width="957" height="292" alt="image" src="https://github.com/user-attachments/assets/59e73246-12cd-4e75-97e6-5f0489841ba0" />

Let's now configure our SMTP relay service.  

### SMTP Relay Service

There are numerous SMTP relay services (Google Workplace, SendGrid, Mailgun, Mailtrap, etc). For this lab, I used [SendGrid](https://www.twilio.com/en-us/sendgrid). Skip the steps below if you used another SMTP relay service.  

To start with SendGrid, you will need to configure the domain name from which your emails will be sent. To do that, go to `Settings > Sender Authentication`, then click on `Authenticate your Domain`:  

<img width="882" height="879" alt="image" src="https://github.com/user-attachments/assets/5f64af73-c8d1-44ea-af8f-d20183f15331" />

After that, specify your phishing domain name, then click on next:  

<img width="1377" height="500" alt="image" src="https://github.com/user-attachments/assets/85512bef-f4d6-4345-8925-008ae2003aa9" />

Then, you will need to add the following DNS records to your domain:  

<img width="1667" height="822" alt="image" src="https://github.com/user-attachments/assets/9d3b9e94-9dc6-428c-8fa0-9c1d8a3d77e9" />

To do that, go back to Namecheap's `Domain List`, then click on `Manage`:  

<img width="1400" height="681" alt="image" src="https://github.com/user-attachments/assets/114d7d72-8de7-4f17-ab6a-d3c14d807a64" />

Next, click on `Advanced DNS`:  

<img width="1358" height="557" alt="image" src="https://github.com/user-attachments/assets/4be1fafb-4a57-4438-a65e-c7da8ad4aa69" />

Finally, go down and click on the `ADD NEW RECORD` button:  

<img width="1104" height="362" alt="image" src="https://github.com/user-attachments/assets/18dcd9d4-7d7d-46c3-9ff0-dc7cc030c5b2" />

After adding all the records highlighted above, go back to SendGrid and check the box `I've added these records`, then click on Verify:  

<img width="1676" height="821" alt="image" src="https://github.com/user-attachments/assets/a7a1651b-3437-4d9d-a4a1-d2882b76bf9e" />

If everything goes as planned, you must see a new column `Status` with the value `Verified`:  

<img width="1878" height="792" alt="image" src="https://github.com/user-attachments/assets/fe8b6822-caa5-455e-9e8d-16c42f07d66c" />

To get the SMTP server information (user, password, email server, etc.), go to `Email API > Integration Guide`, then select `SMTP Relay`:  

<img width="1587" height="630" alt="image" src="https://github.com/user-attachments/assets/2a8ca40d-c15a-41ff-9ec3-be621052200e" />

<br></br>

<img width="1420" height="767" alt="image" src="https://github.com/user-attachments/assets/e7820695-497a-4dbf-b2b9-136bd31d39c9" />

As you can see, the server name and username are respectively **smtp.sendgrid.net** and **apikey**. The password is your API key.  

To generate an API key, go to `Settings > API Keys`, then create a new API Key:  

<img width="1797" height="716" alt="image" src="https://github.com/user-attachments/assets/50ba5422-5606-47a1-b103-831890e8c17e" />

<br></br>

<img width="797" height="362" alt="image" src="https://github.com/user-attachments/assets/bdb74c0d-6dbe-4fed-a025-30b7046e3042" />

Make sure to copy your API Key in a secure place as you won't be able to retrieve it again.  
Well, let's now configure GoPhish's admin panel server.  

### Admin Panel Server

To configure GoPhish, we are going to edit the `config.json` file located in GoPhish root directory.  

Here is its default content:  

<img width="1212" height="607" alt="image" src="https://github.com/user-attachments/assets/086faf45-fdcd-4f0e-b689-53ba46f57b80" />

To start, change the `listen_url` of your Gophish Admin Server to `0.0.0.0:3333` to listen on all interfaces. To do that, you can use your favorite command line editor, or simply use this command:  

```bash
sed -i 's/127.0.0.1/0.0.0.0/g' config.json
```

<img width="1035" height="192" alt="image" src="https://github.com/user-attachments/assets/df6b2638-844a-43fc-8af3-f2544a6fc540" />

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

<img width="972" height="287" alt="image" src="https://github.com/user-attachments/assets/79a251bf-81de-48e2-b854-ae960ef8872f" />

> Do not hesitate to change `$HOME/gophish/` if you installed GoPhish in another directory.  

Once done, you can enable your `GoPhish` service using this command:  

```bash
sudo systemctl enable /etc/systemd/system/gophish.service
```

<img width="1487" height="57" alt="image" src="https://github.com/user-attachments/assets/5d8f790b-880c-4a80-ae35-46894b65de86" />

After that, you can start the service with this command:  

```bash
chmod +x $HOME/gophish/gophish
sudo systemctl start gophish
```

Note that, you must give execution permissions to the `gophish` binary before starting the service, otherwise it will fail to start.

<img width="1822" height="602" alt="image" src="https://github.com/user-attachments/assets/a2e4a2a5-acdd-42fa-8ea7-c22d58f57b35" />

To get GoPhish admin panel's password, run the binary:  

```bash
./gophish
```

<img width="1511" height="237" alt="image" src="https://github.com/user-attachments/assets/6bff6874-a5b9-4822-99ae-33809f34151f" />

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

<img width="1067" height="217" alt="image" src="https://github.com/user-attachments/assets/544db162-37be-4179-a1aa-4daff75d39c7" />

Let's now access GoPhish admin panel:  

<img width="3020" height="1196" alt="image" src="https://github.com/user-attachments/assets/f4464853-9b3b-402e-82a4-e4fb9b0d9d89" />

After specifying your credentials, you will need to reset your password:  

<img width="955" height="601" alt="image" src="https://github.com/user-attachments/assets/779f62d0-1ddf-4f18-b32c-e32242eb2a0a" />

<img width="1222" height="677" alt="image" src="https://github.com/user-attachments/assets/b576d997-17c2-45fc-905c-352e649ac755" />

### Phishing Server

In this section, we are going to configure the phishing server that will host our phishing website.  
By default, this port listens on `0.0.0.0:80`. To access it, you will first need to link your phishing domain with your VPS IP address. This can be done by adding an `A` record to your DNS configuration.  

<img width="1102" height="57" alt="image" src="https://github.com/user-attachments/assets/2a55bedc-e4f2-4858-98f6-05c2a1243862" />

> The **@** symbol represents the root (apex) domain. This is a shorthand for the domain itself (phishlab.xyz), not a subdomain.   

To check if the record was successfully added, use this command:  

```bash
nslookup phishlab.xyz
```

<img width="997" height="187" alt="image" src="https://github.com/user-attachments/assets/6a5c1a29-03ba-43f2-bc51-e679184d2052" />

As you can see, nslookup resolution worked which means that my record was successfully added.  
After that, you should be able to access your phishing domain:  

<img width="597" height="75" alt="image" src="https://github.com/user-attachments/assets/04e44622-43da-4cf8-8eef-b26a58c2f896" />

By default, this returns the default 404 page. However, it works!  

Using an HTTP website for a phishing campaign is not a great idea as it may raise suspicion among employees. To increase the chances of our phishing campaign, we'll add a TLS certificate to our phishing website and configure it to listen on port 443.  

### TLS Certificate

By default, your phishing server listens on port 80, which may trigger warnings in the target's browser.  

<img width="596" height="57" alt="image" src="https://github.com/user-attachments/assets/c3b1e891-f61b-44ef-bd35-08b9c4a96a61" />

To deal with that, let's first install [certbot](https://certbot.eff.org/pages/about):  

```bash
sudo apt install -y certbot
```

<img width="1787" height="420" alt="image" src="https://github.com/user-attachments/assets/38ca12b7-f8a0-4cc6-9cba-a1b35b42808f" />

To generate a new `Let’s Encrypt` certificate, use this command:  

```bash
certbot certonly -d '<your_phishing_domain_name>' --manual --preferred-challenges dns --register-unsafely-without-email
```

<img width="1708" height="780" alt="image" src="https://github.com/user-attachments/assets/05d9ba86-5671-40a1-9b04-cf896de7c211" />

Then, add the `_acme-challenge` TXT record to your DNS configuration.  

<img width="1097" height="51" alt="image" src="https://github.com/user-attachments/assets/5882c579-9bf7-4d49-be94-1f03a15970ed" />

Once done, you can use [Google Admin Toolbox](https://toolbox.googleapps.com/apps/dig/#TXT/) to check if the record was successfully added:  

<img width="1527" height="691" alt="image" src="https://github.com/user-attachments/assets/2b16fe26-cc6c-4c44-ae64-ec212553bf54" />

After that, go back to `certbot` command line, and press `[ENTER]` to continue.  

<img width="1841" height="420" alt="image" src="https://github.com/user-attachments/assets/e090193f-c9ea-47a3-b5d9-96d12a6698f1" />

If everything goes as planned, `certbot` will generate a certificate with its corresponding private key in the `/etc/letsencrypt/live/` directory.  

Then, you can update your `config.json` file by making the following changes:  

- Change `listen_url` to 0.0.0.0:443
- Change `use_tls` to `true`
- Change `cert_path` with the certificate (.pem) generated by certbot
- Change `key_path` with the private key (.pem) generated by certbot

<img width="1587" height="602" alt="image" src="https://github.com/user-attachments/assets/1a06af76-0fe7-4c19-88f0-cd9858f36ec0" />

Once done, you should now be able to access your phishing website using HTTPS:  

<img width="1222" height="582" alt="image" src="https://github.com/user-attachments/assets/99b1d34c-ce60-45f6-8eb6-d4177c48d744" />

Let's now start our first phishing campaign. Shall we?  

### Sending Profiles

**[Sending Profiles](https://docs.getgophish.com/user-guide/documentation/sending-profiles)** is a GoPhish feature that allows you to configure your SMTP relay service. This is where you will specify your SMTP server, username and password, as well as the email address that will be used to send emails to your targets.  

To create a new sending profile, click on the `Sending Profiles` section:  

<img width="3002" height="696" alt="image" src="https://github.com/user-attachments/assets/4526ecc3-7ae9-4ae8-a907-5439e27b82e7" />

Before creating your profile, you will need to verify that you own the email address that will be used by GoPhish for sending phishing emails to your targets.  

If you used SendGrid as a SMTP relay service, go to `Settings > Sender Authentication > Single Sender Verification`:  

<img width="877" height="873" alt="image" src="https://github.com/user-attachments/assets/eca670c4-6e6e-413b-8f58-523e05ca49e0" />

After clicking on `Verify a Single Sender`, click on `Create New Sender`:  

<img width="1678" height="110" alt="image" src="https://github.com/user-attachments/assets/fed9716b-5845-4015-b591-f95d65f96019" />

Then, fill out the fields with your information:  

<img width="1622" height="713" alt="image" src="https://github.com/user-attachments/assets/6db97ef3-3af9-400e-ac71-f2f485dcaf37" />

If everything goes as planned, you must see a new entry in the `Single Sender Verification` section:  

<img width="1678" height="257" alt="image" src="https://github.com/user-attachments/assets/af067a58-781e-46b2-9e72-649d1dd065fc" />

The overall configuration must look like this:  

<img width="1451" height="805" alt="image" src="https://github.com/user-attachments/assets/a9af2641-7fe8-49ac-bd0b-74751a722bb6" />

Once the `Single Sender Verification` configuration done, proceed by adding a new sending profile in GoPhish.  

To do that, complete your sending profile with these information:  

- The host is `smtp.sendgrid.net:587`
- Username is **apikey**
- Password is the API key you generated in the `Settings > API Keys` section
- SMTP From is the email address you configured in the `Single Sender Verification`

> Note that this only works for SendGrid SMTP relay service. For instance, Gmail SMTP relay service configuration will look like [this](https://youtu.be/8Q6EtC8jzpM?si=zNWM14EOkdW7yYgb&t=74).

<img width="1296" height="990" alt="image" src="https://github.com/user-attachments/assets/93af3c84-13d2-4673-a31b-b1d337f5b965" />

To test your sending profile configuration, you can click on `Send Test Email`. This will try to send an email to a target email address of your choice using the SMTP relay service you configured in the `Sending Profile` section.  

To generate a temporary email, you can use [temp-mail](https://temp-mail.org/).  

<img width="576" height="252" alt="image" src="https://github.com/user-attachments/assets/d16b7209-cf27-45c6-af1e-ebc73d02e909" />

After generating your temporary email, click on `Send Test Email`, then fill out the fields and click on Send` to send your test email.  

<img width="1302" height="992" alt="image" src="https://github.com/user-attachments/assets/a6027d12-0013-45d1-bcb2-55d178efb1d7" />

You should normally see this message:  

<img width="687" height="312" alt="image" src="https://github.com/user-attachments/assets/d661a7fd-1651-4ed2-bf83-900b1656ffa3" />

When taking a look to your temporary email's inbox, you should receive an email:  

<img width="720" height="191" alt="image" src="https://github.com/user-attachments/assets/a411cb2b-e4f9-417e-9281-3d6bc63015d2" />

<img width="717" height="331" alt="image" src="https://github.com/user-attachments/assets/f7aec560-0bbf-41c4-960a-61e2a8ca3e29" />

Finally save your changes to avoid losing them.

### Email Templates

**[Email templates](https://docs.getgophish.com/user-guide/documentation/templates)** is the content of the email that is sent to your targets. This is what your targets will read.  

<img width="1300" height="992" alt="image" src="https://github.com/user-attachments/assets/561097d0-ec23-4277-9f8e-6fe88bc57c95" />

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

<img width="680" height="67" alt="image" src="https://github.com/user-attachments/assets/f6d9a977-83a1-430a-a93d-1213e5ee9673" />

### Landing Pages

**[Landing Pages](https://docs.getgophish.com/user-guide/documentation/landing-pages)** are the phishing page that you will use to trick your targets. GoPhish has a feature called `Import Site` that allows you to clone a webpage.  

Let's try to clone [Wordpress.org's login page](https://login.wordpress.org/).  

To do that, click on the `Import Site` button on the `Landing Pages` section:  

<img width="1307" height="763" alt="image" src="https://github.com/user-attachments/assets/11796813-1d41-437e-ac7d-d4c3fd551bcb" />

<br></br>

<img width="686" height="263" alt="image" src="https://github.com/user-attachments/assets/6c82343a-484c-47ee-b121-ae4957197bf7" />

<br></br>

<img width="1297" height="993" alt="image" src="https://github.com/user-attachments/assets/37cd7da6-8392-45bd-a7f9-5f5fc4435320" />

As you can see the page was successfully cloned. To capture credentials, check the "Capture Submitted Data" and "Capture Passwords" boxes. Furthermore, to avoid raising any suspicion, you can redirect the target to a website of your choice:  

<img width="677" height="178" alt="image" src="https://github.com/user-attachments/assets/f424d607-baea-4713-9f93-8c3556b90961" />

After that, save your landing page configuration.  

### Users & Groups

**[Users & Groups](https://docs.getgophish.com/user-guide/documentation/groups)** section is used to specify the target users to which your email will be sent. These users will be placed in various groups depending on their roles, permissions, etc. For instance, the email you will send to executives will not be the same as the email you will send to HR.  

<img width="1301" height="600" alt="image" src="https://github.com/user-attachments/assets/6ce3a30b-5db7-46f7-a85a-6773feeea36e" />

Note that, you can also add users by importing them using a `.csv` file.  

Once done, click on save.  

<img width="1325" height="437" alt="image" src="https://github.com/user-attachments/assets/7b09bbc4-c6b0-45ee-ae6c-bb7e2b150d4d" />


### Campaigns

**[Campaigns](https://docs.getgophish.com/user-guide/documentation/campaigns)** is a feature that is used for sending emails to one or more groups and monitoring for opened emails, clicked links, or submitted credentials.  

To launch your campaign, click on the `Campaigns` section:  

<img width="1303" height="788" alt="image" src="https://github.com/user-attachments/assets/a8555b52-769f-412d-b679-90e97c272adc" />

Make sure to replace the `URL` section with your phishing website URL.  

Before starting your phishing campaign, you can test if everything works properly by clicking on `Send Test Email`. Beware to not send your test email to your real targets. Use instead a [temporary email](https://temp-mail.org/).  

After that, launch your campaign by clicking on the `Launch Campaign` button:  

<img width="1305" height="788" alt="image" src="https://github.com/user-attachments/assets/277a632b-5944-4c75-bb33-48fdbac86f92" />

You should see a dashboard similar to this one:  

<img width="1582" height="876" alt="image" src="https://github.com/user-attachments/assets/dfcbaffa-3795-4059-85ce-e01f2531c1e8" />

When taking a look at the target's mailbox, we can see that they receive our phishing email:  

<img width="713" height="57" alt="image" src="https://github.com/user-attachments/assets/7df07cd2-c87f-48a9-911e-0c472598b2f7" />

Here is the content of the email:  

<img width="700" height="276" alt="image" src="https://github.com/user-attachments/assets/b46a1fd2-e45e-4e36-9eb9-6cd3f13b4a69" />

Let's try to click on the phishing link:  

<img width="1587" height="813" alt="image" src="https://github.com/user-attachments/assets/7ba0bb55-f42b-4aef-80e0-2d76987e8a01" />

We are redirected to the phishing website specified in the `Landing Pages` section.  

When taking a look at the `Campaigns` section, you can see that GoPhish highlighted that the target opened the email address and clicked on the link.  

<img width="1566" height="815" alt="image" src="https://github.com/user-attachments/assets/4d2c464e-026d-433a-8933-d44b9b372701" />

Let's now try to enter some credentials:  

<img width="1583" height="809" alt="image" src="https://github.com/user-attachments/assets/4351e859-09d0-4b44-8ac6-8da96b9ebebf" />

This redirected us to `https://login.wordpress.org` which is the URL we configured in the `Landing Pages` section.  

<img width="1592" height="819" alt="image" src="https://github.com/user-attachments/assets/06c73493-bd4d-4574-9af8-59263effcf12" />

When visualizing our GoPhish campaign dashboard, we can see that the target submitted data:  

<img width="1576" height="812" alt="image" src="https://github.com/user-attachments/assets/41c37c16-b46d-4fe3-b630-90366ad1a849" />

<img width="1565" height="1015" alt="image" src="https://github.com/user-attachments/assets/face8177-59e7-4216-8656-e3ed56b4e3ae" />

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

<img width="1507" height="82" alt="image" src="https://github.com/user-attachments/assets/07aefb94-6367-4b4b-91ae-6e53c24c1a85" />

To install Evilginx using its [binary](https://github.com/kgretzky/evilginx2/releases/latest), follow these steps:  

```bash
wget https://github.com/kgretzky/evilginx2/releases/download/v3.3.0/evilginx-v3.3.0-linux-64bit.zip
```

<img width="1552" height="52" alt="image" src="https://github.com/user-attachments/assets/de13d749-d1f1-4a02-84ce-8a8a1ed9ab4e" />

```bash
unzip evilginx-v3.3.0-linux-64bit.zip -d evilginx
```

<img width="1127" height="207" alt="image" src="https://github.com/user-attachments/assets/f13053ff-ca2f-4c10-a64d-603304a790bf" />

After that, give `evilginx` execution permissions:  

```bash
chmod +x ./evilginx
```

<img width="977" height="80" alt="image" src="https://github.com/user-attachments/assets/79f9808a-580a-4f50-85b7-71d2e6cfcb09" />

Once done, launch `evilginx`:  

```bash
./evilginx
```

<img width="1674" height="951" alt="image" src="https://github.com/user-attachments/assets/7ed52dc8-bc9d-461c-ba4b-a28a8f5fc967" />

As you can see, Evilginx failed to start a DNS server on `port 53`. This occured because the port is being used by another process on the system. To check it, use this command:  

```bash
sudo lsof -i :53
```

<img width="1211" height="157" alt="image" src="https://github.com/user-attachments/assets/8034fbc2-b6f4-48d4-823c-736cb5213a26" />

To deal with that, you will first need to stop the `systemd-resolved` service, then remove the `/etc/resolv.conf` file:  

```bash
sudo systemctl stop systemd-resolved.service
```

```bash
lsof -i :53
```

<img width="877" height="52" alt="image" src="https://github.com/user-attachments/assets/5495645b-b7f4-4709-8305-e1e4dc0bf94a" />

```bash
mv /etc/resolv.conf /etc/resolv.conf.bak
```

<img width="901" height="30" alt="image" src="https://github.com/user-attachments/assets/7a3755ec-0c98-4c07-86d2-12502c8a8f5d" />

After that, execute the following command to create a new `/etc/resolv.conf` with your favorite recursive DNS servers:  

```bash
echo -e 'nameserver 1.1.1.1\nnameserver 9.9.9.9' >> /etc/resolv.conf
```

<img width="982" height="82" alt="image" src="https://github.com/user-attachments/assets/160d521d-fdbb-40f5-91d7-7db82cfd366f" />

To check if the DNS resolution works, you can perform an `nslookup`:  

```bash
nslookup google.com
```

<img width="1455" height="657" alt="image" src="https://github.com/user-attachments/assets/82f2f258-5b78-42e4-adf8-f9e454b7f8fa" />

See that Evilginx uses port `tcp/443` to host your phishing website, you will need to reconfigure your GoPhish's phishing server URL to listen on another port (eg: tcp/8843).  

<img width="1422" height="602" alt="image" src="https://github.com/user-attachments/assets/370c6449-850b-4458-be6b-c80ae873d5e7" />

After that, restart your Gophish service to apply the changes:  

```bash
systemctl restart gophish
```

```bash
systemctl status gophish
```

<img width="1671" height="255" alt="image" src="https://github.com/user-attachments/assets/2a7a18cd-4592-4a4d-bf7e-cba18e739166" />

Let's now configure the domain, and the external IPv4 address:  

```
config domain <your_phishing_domain_name>
```

<img width="977" height="57" alt="image" src="https://github.com/user-attachments/assets/bee72247-9747-46d2-87a9-7970446b87ce" />

```
config ipv4 external <your_phishing_domain_ipv4_address>
```

<img width="792" height="52" alt="image" src="https://github.com/user-attachments/assets/c6e633a2-4e8d-401d-abbe-84a18c23712f" />

Enter the `Help` command to get some help:  

<img width="1242" height="325" alt="image" src="https://github.com/user-attachments/assets/a942c44a-d7b6-4a2b-a203-415da9e3de61" />

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
