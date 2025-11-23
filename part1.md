Chapter 1 — Install & Run Apache2 on WSL Ubuntu

1. Update Ubuntu

sudo apt update && sudo apt upgrade -y

2. Install Apache2

sudo apt install apache2 -y

3. Start Apache2


sudo service apache2 start

Check service status:

sudo service apache2 status

4. Test Apache2 in Windows Browser

hostname -I

Visit in Chrome:

IMPORTANT: Fix Windows Port Binding

WSL sometimes cannot use ports (80/443) if Windows services block them.

Check if another service is using port 80:

Open CMD:

netstat -ano | findstr :80

If something is using it (like “World Wide Web Publishing Service”), disable it:

sc stop W3SVC
sc config W3SVC start= disabled

Then restart Apache:

sudo service apache2 restart

5. Apache Document Root**

Default web folder:

/var/www/html

Edit index file:

sudo nano /var/www/html/index.html

6. Allow Apache2 Through Windows Firewall

powershell
New-NetFirewallRule -DisplayName "WSL Apache Port 80" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 80

