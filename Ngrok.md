# 📘 Ngrok Documentation

## 🧠 What is Ngrok?

**Ngrok** is a secure tunneling service that allows you to expose a local development server to the internet. It creates a secure tunnel from a public endpoint (a unique URL) to your locally running web service.

> ✅ Ideal for testing webhooks, exposing local APIs, demos, or accessing a local application remotely.

---

## 🚀 Key Features

* ✅ **HTTPS Tunnels** to localhost
* ✅ **Custom Subdomains**
* ✅ **Reserved Domains**
* ✅ **Basic Authentication**
* ✅ **Request Inspection Dashboard**
* ✅ **Webhook replay**
* ✅ **TCP/UDP tunneling (paid)**
* ✅ **Custom Headers & IP Restrictions**

---

## 🔧 How Ngrok Works

When you run `ngrok` with a local port, it:

1. Establishes a secure tunnel to Ngrok's cloud servers.
2. Ngrok assigns a publicly accessible URL.
3. Traffic is forwarded from the public URL to your local machine.

---

## 💻 Installation

### 🧑‍💻 Prerequisites:

* Local development server (Node, Python, etc.)
* Internet connection
* Ngrok account (optional for free-tier usage)

### 📦 Step-by-Step Installation

#### 🔹 **Linux / macOS**

```bash
# Download ngrok (replace with latest version link)
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
unzip ngrok-stable-linux-amd64.zip
sudo mv ngrok /usr/local/bin
```

#### 🔹 **Windows**

* Download from: [https://ngrok.com/download](https://ngrok.com/download)
* Extract the executable and place it in your system `PATH`.

---

## 🔐 Connect Your Ngrok Account (Optional but Recommended)

After creating an account on [https://ngrok.com](https://ngrok.com):

```bash
ngrok config add-authtoken <your_auth_token>
```

You can find the token in your Ngrok dashboard → Setup & Installation section.

---

## 🧪 Basic Usage Examples

### ✅ HTTP Tunneling

```bash
# Expose local port 3000 to the internet
ngrok http 3000
```

Output:

```
Forwarding https://abcd-1234.ngrok.io -> http://localhost:3000
```

### ✅ TCP Tunneling (Paid Plans)

```bash
ngrok tcp 22
```

Used to expose SSH or other TCP services.

---

## ⚙️ Advanced Configuration

You can use a config file (`~/.ngrok2/ngrok.yml`) to manage multiple tunnels or set default values.

### 🛠 Sample `ngrok.yml`

```yaml
authtoken: <your_auth_token>

tunnels:
  webapp:
    addr: 3000
    proto: http
    hostname: demo.example.com  # for reserved domains (paid)

  ssh:
    addr: 22
    proto: tcp
```

Then start:

```bash
ngrok start webapp
```

---

## 🛡️ Security Features

* **Basic Auth**:

  ```bash
  ngrok http -auth="user:password" 3000
  ```

* **IP Restrictions** (Pro+ plans)

* **Custom Domains** (Reserved domains)

* **Webhook Replay** from the Ngrok dashboard

---

## 📊 Web Interface Dashboard

Ngrok runs a local dashboard on:

```
http://127.0.0.1:4040
```

You can:

* Inspect requests/responses
* Replay failed requests
* Debug APIs (e.g., webhooks from Stripe, GitHub)

---

## 🌍 Common Use Cases

* 🧪 Testing webhooks (Stripe, Razorpay, GitHub)
* 🌐 Demoing apps without deploying
* 🔐 Exposing local backend for frontend integration
* 🚧 Quick public testing before production deployment
* 🧩 IoT device local access
* 🐞 Debugging client-server issues

---

## 🔄 Persistent Tunnels (Reserved Domains)

Ngrok free tunnels **change URLs each time**. To avoid updating webhooks/dev URLs constantly:

* Use **reserved domains** (requires a paid plan):

```yaml
tunnels:
  myapp:
    proto: http
    addr: 3000
    hostname: myapp.reetesh.dev  # Reserved in Ngrok dashboard
```

➡ This ensures the tunnel endpoint is **stable**, ideal for long-term webhook integrations.

---

## 🛜 Exposing Services Behind NAT/Firewalls

Ngrok is great when:

* You're on a private network (e.g. home Wi-Fi, office)
* Behind a corporate firewall or NAT
* No access to public IPs or port forwarding

> This makes it ideal for **IoT, remote debugging**, or when working from restrictive environments.

---

## 👥 Team & Collaboration Support

In **Ngrok Teams or Business plans**:

* Share tunnels with teammates
* Team-wide authentication
* Manage multiple team environments via **Ngrok API**

Use it for **collaborative development**, QA testing, etc.

---

## 🧰 DevOps & CI/CD Integration

You can:

* Expose local services in CI jobs (e.g., GitHub Actions or Bitbucket Pipelines)
* Automatically test **webhooks** in test pipelines
* Script tunnel creation with the **Ngrok API**

### 🔧 Sample GitHub Actions Integration

```yaml
steps:
  - name: Start Ngrok Tunnel
    run: |
      ./ngrok config add-authtoken ${{ secrets.NGROK_AUTH_TOKEN }}
      ./ngrok http 3000 > /dev/null &
```

---

## 🌍 DNS Configuration (Custom Domains)

To point your **own domain** (like `dev.reetesh.com`) to an Ngrok tunnel:

1. Add DNS CNAME:

   ```
   dev.reetesh.com -> cname.ngrok.io
   ```
2. Configure in `ngrok.yml`:

   ```yaml
   hostname: dev.reetesh.com
   ```
3. Works only on **paid plans**.

---

## 🕵️‍♂️ Inspect & Replay Webhooks

Ngrok dashboard (`http://127.0.0.1:4040`) lets you:

* View HTTP headers, status codes, and body
* Replay failed webhook requests
* Debug issues live

This is extremely helpful for **Stripe, Razorpay, GitHub, Twilio**, etc.

---

## 📈 Analytics & Logs (Enterprise)

Paid users get:

* Request logs over time
* Rate limits monitoring
* IP & geo-based analytics
* Alerts for abnormal activity

---

## 🔒 Security Best Practices

* Use `-auth` to secure tunnels (e.g., for internal dashboards)
* Restrict by IP using `allow_cidrs` in `ngrok.yml`
* Rotate your Ngrok **authtokens** periodically
* Do **not expose admin panels or DBs** directly without protection

---

## 📡 Ngrok Alternatives: Quick Comparison

| Feature             | Ngrok    | Cloudflare Tunnel | LocalTunnel | Expose.dev |
| ------------------- | -------- | ----------------- | ----------- | ---------- |
| Free plan available | ✅        | ✅                 | ✅           | ✅          |
| Custom domain       | Paid     | ✅                 | ❌           | ✅          |
| Auth + IP filters   | ✅ (Paid) | ✅                 | ❌           | ✅          |
| UI / Dashboard      | ✅        | ❌                 | ❌           | ✅          |
| Open Source         | ❌        | ❌                 | ✅           | ✅          |

---

## 📂 Directory Structure for Projects

For teams using Ngrok with config files:

```
project-root/
│
├── ngrok.yml               # Tunnel definitions
├── scripts/
│   └── start-ngrok.sh      # Starts tunnels for dev/test
└── README.md               # Document usage
```

---

## 🧩 Alternatives to Ngrok

| Tool                  | Free Tier | Auth Support | Custom Domain | Notes                     |
| --------------------- | --------- | ------------ | ------------- | ------------------------- |
| **Ngrok**             | ✅         | ✅            | Paid Plan     | Most popular, reliable    |
| **LocalTunnel**       | ✅         | ❌            | ❌             | Very simple & open source |
| **Cloudflare Tunnel** | ✅         | ✅            | ✅             | Complex setup, powerful   |
| **Expose.dev**        | ✅         | ✅            | ✅             | Open source, good UI      |

---

## 🧯 Troubleshooting

| Issue                     | Solution                                                       |
| ------------------------- | -------------------------------------------------------------- |
| “Tunnel session failed”   | Check internet or login token                                  |
| “Port already in use”     | Kill the conflicting process or use another port               |
| Custom domain not working | Ensure you’ve added DNS record pointing to Ngrok’s CNAME or IP |
| Webhook not triggering    | Check tunnel is running and correct endpoint is exposed        |
| 403 Forbidden (on auth)   | Use correct `-auth=user:pass` format or check `ngrok.yml`      |

---

## 🧾 Final Notes

* Ngrok’s free plan provides **1 tunnel** and **40 connections/min**.
* Paid plans unlock:

  * Multiple tunnels
  * Reserved domains
  * IP filtering
  * White-label domains
  * Higher rate limits

---

## 🔗 Useful Links

* 🧭 Official Site: [https://ngrok.com](https://ngrok.com)
* 📘 Docs: [https://ngrok.com/docs](https://ngrok.com/docs)
* 🐙 GitHub (unofficial forks): [https://github.com](https://github.com)
* 🌐 Alternatives: [https://alternativeto.net/software/ngrok/](https://alternativeto.net/software/ngrok/)
