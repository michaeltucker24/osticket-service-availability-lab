# osTicket Service Availability Lab

## Overview

This repository documents a support-style troubleshooting scenario where users are unable to access an osTicket web interface hosted on a Linux server.

The purpose of this project is to practice service availability troubleshooting, web service validation, network access checks, log review, and customer-facing technical documentation.

## Scenario

Users report that the osTicket web interface is unavailable from their browser.

The issue may involve the web server service, application availability, firewall rules, cloud network rules, or local service configuration.

## Objectives

- Confirm whether the web server is running
- Check whether the service is listening on the expected port
- Review logs for service or application errors
- Test local and external web access
- Verify firewall or cloud network rules
- Identify the root cause
- Resolve the access issue
- Document verification and customer-facing update

## Environment

- Application: osTicket
- OS: Ubuntu Linux / Linux server environment
- Web Server: Apache or Nginx
- Platform: Cloud-hosted VM / Local VM lab
- Tools: `systemctl`, `journalctl`, `ss`, `curl`, `ufw`

## Skills Demonstrated

- Web service troubleshooting
- Linux service diagnostics
- Log analysis
- Port validation
- Firewall and network rule review
- Ticket-style support documentation
- Customer-facing technical communication

## Support Scenario Summary

| Area | Details |
|---|---|
| Reported Issue | Users cannot access osTicket from a browser |
| Affected Service | osTicket web interface |
| Possible Causes | Web service stopped, blocked firewall port, cloud network rule, service not listening |
| Key Tools | `systemctl`, `journalctl`, `ss`, `curl`, `ufw` |
| Support Focus | Service availability, root cause analysis, verification, customer update |

## Investigation Workflow

### 1. Check web server status

For Apache:

```bash
sudo systemctl status apache2
```

For Nginx:

```bash
sudo systemctl status nginx
```

### 2. Review service logs

For Apache:

```bash
sudo journalctl -u apache2
```

For Nginx:

```bash
sudo journalctl -u nginx
```

### 3. Confirm listening ports

```bash
sudo ss -tuln
```

Check for web ports:

```bash
sudo ss -tuln | grep ':80\|:443'
```

### 4. Test local web access

```bash
curl -I http://localhost
```

### 5. Check firewall rules

```bash
sudo ufw status verbose
```

### 6. Allow web traffic if needed

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw reload
```

### 7. Test external access

```bash
curl -I http://server-ip
```

## Commands Used

```bash
sudo systemctl status apache2
sudo systemctl status nginx
sudo journalctl -u apache2
sudo journalctl -u nginx
sudo ss -tuln
sudo ss -tuln | grep ':80\|:443'
curl -I http://localhost
sudo ufw status verbose
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw reload
curl -I http://server-ip
```

## Root Cause Example

The web service was running locally, but external access was blocked by a firewall or cloud network security rule.

## Resolution Example

The required inbound web traffic rule was added to allow HTTP and/or HTTPS access.

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw reload
```

If the web server was stopped, it was restarted:

```bash
sudo systemctl restart apache2
```

or:

```bash
sudo systemctl restart nginx
```

## Verification

The issue was verified as resolved by confirming:

- The web server service was active
- The service was listening on the expected port
- Local access returned a valid HTTP response
- Firewall rules allowed HTTP/HTTPS traffic
- External browser or `curl` access succeeded

Example verification command:

```bash
curl -I http://server-ip
```

Expected result:

```text
HTTP/1.1 200 OK
```

## Customer-Facing Update

The osTicket access issue was resolved. The web service was running, but external access was blocked by a firewall or network access rule. The required web traffic rule was corrected, and the osTicket interface is now reachable.

## Lessons Learned

This lab reinforced that service availability troubleshooting should check both local service health and external network access. A web application can be running correctly on the server but still be unreachable if firewall or cloud network rules block traffic.

## Portfolio Note

This project is part of my Linux Support Engineer portfolio. It demonstrates practical troubleshooting, documentation, and support workflow skills relevant to Ubuntu/Linux support roles.
