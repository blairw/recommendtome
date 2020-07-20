## Recommended installation of AMP webserver stack on macOS

### macOS Catalina

Based on the [Grav blog guide](https://getgrav.org/blog/macos-catalina-apache-multiple-php-versions) but omitting:

- Homebrew setup (this is assumed)
- Installation of Visual Studio Code or VSCodium to enable `code` command (this is assumed)
- Muliple versions of PHP
- Virtual hosts
- APC caching
- YAML
- Xdebug

If you need any of those things, please refer to the Grav blog guide.

#### Part 1


1. Run `brew doctor` just in case
2. The following (note: you will need to enter admin password):

    ```bash
    brew install openldap libiconv \
        && sudo apachectl stop \
        && sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null \
        && brew install httpd \
        && sudo brew services start httpd
    ```

3. Edit the httpd configuration - `code /usr/local/etc/httpd/httpd.conf`

    - `Listen 8080` &rarr; `Listen 80`
    - `DocumentRoot "/usr/local/var/www"` &rarr; (whatever location you want to use)
    - `<Directory ...>` &rarr; (whatever location you want to use)
        - set `AllowOverride All`
        - enable `LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so`
    - `User your_user`, `Group staff`
    - `ServerName localhost`