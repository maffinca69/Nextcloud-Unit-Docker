# Nextcloud-Unit-Docker
Nextcloud + Unit = Better speed 🔥

Many people know that Nextcloud is not known for its performance
This repository allows you to get the most performance out of your Nextcloud

### Why is this solution fast?
1. Instead of the standard Apache, the new performance Nginx Unit is used
2. Postgresql is used instead of SQLite / MySQL
3. Redis based caching is used (APCu is not used for ease of support).
4. alpine versions of postgres and redis containers are used. Less weight - more speed
5. Use current version of php with OPCache enabled

### Recommendations
In config/config.php enable logging of critical errors only. This way, Nextcloud will make fewer log entries
Disable unnecessary standard applications and plugins

### What is the speed in the end?
With a regular docker container all-in-one on my server, the load took about 2-3sec. With the new configuration it takes about 1s to boot up

### My server specifications
* Xeon 2640 v4 (10 core, 20 threads)
* 16 GB ECC RAM
* 256 SSD NVME (Samsung 970 EVO)
* 1GB Ethernet
* Debian 12

### Pre-requirements
To run it, you need to download the archive with the latest version from the official website https://download.nextcloud.com/server/releases/.
After downloading, put the files of this repository in one folder.

### Requirements
* Docker
* Cron (on host)

### Installation
* docker-compose up -d
* In the cron entry on your host machine, you need to add the entry
```sh
*/5 * * * * * * docker exec -u $(id -u unit) nextcloud_unit_1 php cron.php
```
**unit - owner of config/config.php file**
