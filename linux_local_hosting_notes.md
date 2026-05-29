# Hosting Websites Locally in Linux

So, in this section we are going to learn different ways to host a website locally using the Linux terminal. We will use:

- Python
- PHP
- NPX (`http-server`)
- Apache2
- Curl
- Wget

These methods are useful for:
- Testing websites
- Running projects quickly
- Learning networking basics
- Local development

---

# 1. Hosting with Python

Python has a built-in HTTP server, so we can start a local web server instantly.

## Basic Command

```bash
python3 -m http.server
```

By default, this starts the server on port `8000`.

To access it:

```text
http://localhost:8000
```

Open that in your browser.

---

## Changing the Port Number

```bash
python3 -m http.server 7000
```

Now the server runs on port `7000`.

Access it with:

```text
http://localhost:7000
```

The server automatically hosts files from the current directory where the command is executed.

---

# 2. Hosting with PHP

PHP also provides a simple built-in server.

## Command

```bash
php -S 127.0.0.1:8000
```

Explanation:
- `127.0.0.1` → loopback IP address (localhost)
- `8000` → port number

You can change the port if needed:

```bash
php -S 127.0.0.1:9000
```

Access it from:

```text
http://localhost:9000
```

---

# 3. Hosting with NPX (`http-server`)

If Node.js is installed, we can use `http-server`.

## Command

```bash
npx http-server -p 8086
```

Explanation:
- `-p` specifies the port number
- `8086` is just an example

Access it from:

```text
http://localhost:8086
```

This is useful for:
- Static websites
- Frontend testing
- Quick deployments

---

# 4. Hosting with Apache2

Apache2 is one of the most widely used web servers.

It is commonly used for:
- Web hosting
- Testing web applications
- Running production servers

---

## Installing Apache2

```bash
sudo apt install apache2
```

---

## Starting Apache2

```bash
sudo systemctl start apache2
```

To check status:

```bash
sudo systemctl status apache2
```

---

## Default Port

Apache2 runs on port `80` by default.

Access it from:

```text
http://localhost
```

---

## Changing the Port Number

Apache configuration files are usually located in:

```bash
/etc/apache2/ports.conf
```

Open it using any editor:

```bash
sudo nano /etc/apache2/ports.conf
```

Change:

```text
Listen 80
```

To:

```text
Listen 8080
```

Then restart Apache:

```bash
sudo systemctl restart apache2
```

Now access it with:

```text
http://localhost:8080
```

---

# 5. Using Curl

`curl` is a command-line tool used to access websites and APIs directly from the terminal.

## Basic Usage

```bash
curl https://example.com
```

This fetches the webpage content directly in the terminal.

---

## Access Localhost with Curl

```bash
curl http://localhost:8000
```

Useful for:
- Testing APIs
- Checking server responses
- Debugging websites
- Downloading files

---

# 6. Using Wget

`wget` is a command-line tool used to download files directly from the internet or servers.

It is very useful for:
- Downloading files
- Downloading websites
- Testing downloads
- Fetching backups
- Automating downloads in scripts

---

## Basic Usage

```bash
wget https://example.com/file.zip
```

This downloads the file into the current directory.

---

## Download and Rename File

```bash
wget -O newname.zip https://example.com/file.zip
```

Explanation:
- `-O` allows us to save the file with a custom name

---

## Resume Interrupted Downloads

```bash
wget -c https://example.com/file.zip
```

Explanation:
- `-c` continues/resumes the download

Very useful for large files.

---

## Download Website HTML

```bash
wget https://example.com
```

This downloads the HTML page.

---

## Mirror/Clone a Website

```bash
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent https://example.com
```

Explanation:
- `--mirror` → mirror the site
- `--convert-links` → fix links for offline browsing
- `--page-requisites` → download CSS/images/scripts
- `--no-parent` → avoid going to parent directories

Used for:
- Offline browsing
- Website backups
- Learning web structure

---

## Download in Background

```bash
wget -b https://example.com/file.iso
```

Explanation:
- `-b` runs the download in background

Check logs with:

```bash
tail -f wget-log
```

---

## Limit Download Speed

```bash
wget --limit-rate=500k https://example.com/file.zip
```

Useful when:
- Internet is slow
- Avoiding bandwidth overuse

---

# Difference Between Curl and Wget

| Tool | Main Purpose |
|---|---|
| curl | Access APIs and fetch responses |
| wget | Download files/websites |

---

# Quick Comparison

| Method | Best For | Easy Level |
|---|---|---|
| Python HTTP Server | Quick testing | Very Easy |
| PHP Server | PHP projects | Easy |
| NPX HTTP Server | Frontend/static sites | Easy |
| Apache2 | Real web server setup | Medium |
| Curl | Testing/debugging | Easy |
| Wget | Downloading files/websites | Easy |

---

# Important Notes

- `localhost` and `127.0.0.1` both refer to your own machine.
- Ports below `1024` often require sudo privileges.
- Make sure firewall rules are not blocking ports.
- Always stop unused servers to avoid port conflicts.

---

# Common Commands Summary

```bash
# Python
python3 -m http.server 7000

# PHP
php -S 127.0.0.1:8000

# NPX
npx http-server -p 8086

# Install Apache2
sudo apt install apache2

# Start Apache2
sudo systemctl start apache2

# Restart Apache2
sudo systemctl restart apache2

# Curl
curl http://localhost:8000

# Wget
wget https://example.com/file.zip
```
