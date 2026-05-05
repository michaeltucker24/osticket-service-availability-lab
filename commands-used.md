# Commands Used

This file lists the primary commands used throughout the osTicket Service Availability Lab.

## Check web server status

Apache:

```bash
sudo systemctl status apache2
```

Nginx:

```bash
sudo systemctl status nginx
```

## Review web server logs

Apache:

```bash
sudo journalctl -u apache2
```

Nginx:

```bash
sudo journalctl -u nginx
```

## Restart web server

Apache:

```bash
sudo systemctl restart apache2
```

Nginx:

```bash
sudo systemctl restart nginx
```

## Enable web server at boot

Apache:

```bash
sudo systemctl enable apache2
```

Nginx:

```bash
sudo systemctl enable nginx
```

## Check listening ports

```bash
sudo ss -tuln
sudo ss -tuln | grep ':80\|:443'
```

## Test local web access

```bash
curl -I http://localhost
curl -v http://localhost
```

## Test external web access

```bash
curl -I http://server-ip
curl -v http://server-ip
```

## Check firewall rules

```bash
sudo ufw status verbose
```

## Allow HTTP and HTTPS traffic

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw reload
```

## Check recent system errors

```bash
journalctl -p 3 -xb
```
