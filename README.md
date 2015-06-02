
# Automatic IP Filter by DNS Resolution

The purpose of this PHP script is to periodically refresh an .htaccess IP filter with the result of a DNS lookup.  This is useful for managing filters for field technicians with dynamic IP addresses.

This script works by scanning .htaccess files for lines starting with "# DYNDNS", then update the trailing "Allow from x.x.x.x" line with the current IP address.

## Installation

Add the .htaccess.dyndns.php file to any folder with an .htaccess file that you wish to update.

- The script will only open an .htaccess file located within the same folder.
- Each folder you wish to update will require a separate copy.

## .htaccess Configuration

Edit your .htaccess file and add the "# DYNDNS" instruction before each "Allow" statement.

	Order Deny,Allow
	Deny from all

	# DYNDNS mydns.dynamic-dns.com
	Allow from 192.168.1.1

Add Notes for reference

	# DYNDNS mydns.dynamic-dns.com - John in Colorado
	Allow from 192.168.1.1

## Cron Setup

Setup a cron job that will run every 30 minutes (or whatever) to update the file.

	30 * * * *
	php -q /home/account/public_html/.htaccess.dyndns.php > /dev/null
