# Changelog

## v3.9.7 - 2019-08-02

### Added

- MySQL configuration tuning
- Cronjob to optimize MySQL databases weekly
- WO-kernel systemd service to automatically apply kernel tweaks on server startup
- Proftpd stack now secured with TLS
- New Nginx package built with Brotli from operating system libraries
- Brotli configuration with only well compressible MIME types
- WordPress site url automatically updated to `https://domain.tld` when using `-le/--letsencrypt` flag
- More informations during certificate issuance about validation mode selected
- `--php72` as alternative for `--php`
- Automated removal of the deprecated variable `ssl on;` in previous Nginx ssl.conf
- Project Contributing guidelines
- Project Code of conduct

### Changed

- `wo maintenance` refactored
- Improved debug log
- Updated Nginx configuration process to not overwrite files with custom data (htpasswd-wo, acl.conf etc..)
- Adminer updated to v4.7.2
- eXtplorer updated to v2.1.13
- Removed WordOps version from the Nginx header X-Powered-By to avoid possible security issues
- Several code quality improvements to speed up WordOps execution
- Few adjustements on PHP-FPM configuration (max_input_time,opcache.consistency_checks)
- Added /dev/urandom & /dev/shm to open_basedir in PHP-FPM configuration

### Fixed

- Kernel tweaks were not applied without server reboot
- Fail2ban standalone install
- `wo stack purge --all` error due to PHP7.3 check
- Nginx helper configuration during plugin install for Nginx fastcgi_cache and redis-cache
- phpRedisAdmin stack installation
- Fixed Travis CI build on pull requests
- Nginx `server_names_hash_bucket_size` variable error after WordOps upgrade

## v3.9.6.2 - 2019-07-24

### Changed

- Improve `wo update` process duration
- Improve package install/upgrade/remove process

### Fixed

- phpMyAdmin archive download link archive
- Arguments `--letsencrypt=clean/purge`
- Incorrect directory removal during stack upgrade

## v3.9.6.1 - 2019-07-23

### Fixed

- Typo in  `--letsencrypt=subdomain`
- phpMyAdmin upgrade archive extraction
- Error in the command `wo update`. Please `wo update --beta` as workaround

## v3.9.6 - 2019-07-20

### Added

- New Nginx package on Ubuntu with Cloudflare HTTP/2 HPACK and Dynamic TLS records
- phpMyAdmin upgrade with `wo stack upgrade --phpmyadmin`
- Wildcard SSL Certificates support with DNS validation
- Let's Encrypt DNS API support (Cloudflare, DigitalOcean, etc ..) on domain, subdomain, and wildcard
- Flag `--letsencrypt=clean` to purge a previous SSL configuration
- Support for Debian 10 buster (testing - not ready for production)
- Fail2ban with custom jails to secure WordPress & SSH
- Variable `keylength` in /etc/wo/wo.conf to define letsencrypt certificate keylenght
- ProFTPd stack with UFW & Fail2ban configurationz
- Beta branch and command `wo update --beta` for beta releases
- Extra directives in wp-config.php (limit posts revisions, set max_memory, enable auto-update for minor-releases)

### Fixed

- Nginx was not reloaded after enabling HSTS
- Netdata, Composer & Fail2Ban stack remove and purge
- WordPress not installed by `wo site update` with basic php73 sites

## v3.9.5.4 - 2019-07-13

### Added

- New Nginx package on Ubuntu with TLS v1.3 support (OpenSSL 1.1.1c)
- Netdata upgrade with `wo stack upgrade --netdata`
- Netdata stack remove/purge

### Changed

- phpRedisAdmin is now installed with the stack `--admin`
- Remove memcached - not required anymore

### Fixed

- phpRedisAdmin installation
- Duplicated locations /robots.txt after upgrade to v3.9.5.3
- Let's Encrypt stack `wo site update --letsencrypt/--letsencrypt=off`
- pt-query-advisor dead link
- Netdata persistant configuration

## v3.9.5.3 - 2019-06-18

### Added

- Argument `--preserve` with the command `wo update` to keep current Nginx configuration

### Fixed

- Nginx upgrade failure when running wo update

## v3.9.5.2 - 2019-06-17

### Added

- Non-interactive install/upgrade
- Argument `--force` with the command `wo update`
- Argument `-s|--silent` to perform non interactive installation

### Changed

- robots.txt location block moved from locations-wo.conf to wpcommon(-php7).php

### Fixed

- WP_CACHE_KEY_SALT set twice with wpredis
- WordOps version check when using `wo update`
- robots.txt file download if not created
- PHP-FPM socket path in stub_status.conf : PR [#82](https://github.com/WordOps/WordOps/pull/82)

## v3.9.5.1 - 2019-05-10

### Fixed

- Adminer download link

## v3.9.5 - 2019-05-02

### Added

- IPv6 support with HTTPS
- Brotli support in Nginx
- Let's Encrypt support with --proxy
- Install script handle migration from EEv3
- load-balancing on unix socket for php-fpm
- stub_status vhost for metrics
- `--letsencrypt=subdomain` option
- opcache optimization for php-fpm
- EasyEngine configuration backup before migration
- EasyEngine configuration cleanup after migration
- WordOps configuration backup before upgrade
- Previous acme.sh certs migration
- "wo maintenance" command to perform server package update & cleanup
- Support for Netdata on backend : https://server.hostname:22222/netdata/
- New Stacks : composer and netdata
- additional argument for letsencrypt : --hsts
- Clean Theme for adminer
- Credits for tools shipped with WordOps
- Cache exception for Easy Digital Download
- Additional cache exceptions for Woocommerce
- MySQL monitoring with Netdata
- WordOps-dashboard on 22222, can be installed with `wo stack install`
- Extplorer filemanager in WordOps backend
- Enable OSCP Stapling with Let's Encrypt
- Compress database backup with pigz (faster than gzip) before updating sites
- Support for Ubuntu 19.04 (disco) - few php extensions missing
- Support for Raspbian 9 (stretch) - tested on Raspberry Pi 3b+
- backup letsencrypt certificate before upgrade
- directives emergency_restart_threshold & emergency_restart_interval to restart php-fpm in case of failure
- EasyEngine cronjob removal during install
- Kernel tweaks via systctl.conf
- open_basedir on php-fpm process to forbid access with php outside of /var/www & /run/nginx-cache

### Changed

- letsencrypt stack refactored with acme.sh
- letsencrypt validation with webroot folder
- hardened nginx ssl_ecdh_curve
- Update phpredisadmin
- Increase MySQL root password size to 24 characters
- Increase MySQL users password size to 24 characters
- Nginx locations template is the same for php7.2 & 7.3
- backend SSL configuration now stored in /var/www/22222/conf/nginx/ssl.conf
- Install Netdata with static pre-built binaries instead of having to compile it from source
- Nginx updated to new stable release (1.16.0)
- New packages (phpmyadmin, adminer, composer) are not download in /tmp anymore

### Fixed

- PHP 7.3 extras when php 7.2 isn't installed
- acme.sh installation
- acme.sh alias with config home variable
- deb.sury.org repository gpg key
- Nginx upgrade from previous WordOps release
- Force new Nginx templates during update
- Error message about missing my.cnf file during upgrade
- PHP 7.2 & PHP 7.3 pool configuration during upgrade
- WordOps backup directory creation before upgrade
- EasyEngine database sync during migration
- fix command "wo info"
- phpmyadmin install with composer
- command "wo clean --memcached"
- phpredisadmin setup
- --hsts flag with basic html site
- hsts flag on site not secure with letsencrypt
- fix import of previous acme.sh certificate
- fix proxy webroot folder creation

## v3.9.4 - 2019-03-15

### Added

- Nginx module nginx_vts
- Migration script from nginx-ee to nginx-wo
- Support for Debian 9 (testing)
- New Nginx build v1.14.2

### Changed

- Update WP-CLI version to 2.1.0
- Update Adminer to 4.6.2
- Update predis to v1.1.1
- Refactored nginx.conf
- Removed HHVM Stack
- Removed old linux distro checks
- Replace wo-acme-sh by acme.sh

### Fixed

- Outdated Nginx ssl_ciphers suite
- Debian 9 nginx build

## v3.9.3 - 2019-03-07

### Changed

- Updated Nginx fastcgi_cache templates
- Updated Nginx redis_cache templates
- Updated Nginx wp-super-cache templates
- Updated Nginx configuration for WordPress 5.0
- remove --experimental args
- MariaDB version bumped to 10.3
- Refactored Changelog
- Updated WO manual
- Updated WO bash_completion
- Refactored README.md

### Added

- Add WebP image support with Nginx mapping
- Add PHP 7.3 support
- WordPress $skip_cache variable mapping

### Fixed

- Nginx variable $webp_suffix on fresh install ([#21](https://github.com/WordOps/WordOps/issues/21))
- wo update command ([#7](https://github.com/WordOps/WordOps/issues/7))
- Fix php services management ([#12](https://github.com/WordOps/WordOps/issues/12))
- Fix WP-CLI install

## v3.9.2 - 2018-11-30

### Changed

- Re-branded the fork to WordOps
- Codebase cleanup
- Set PHP 7.2 as the default
- Included support for newer OS releases
- Reworked the HTTPS configuration
- Added more automated testing with Redis
- Replaced Postfix with smtp-cli
- Dropped mail services
- Dropped w3tc support