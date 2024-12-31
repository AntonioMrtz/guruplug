# Update repository sources

The GuruPlug comes with Debian 5 installed, which reached its end of life some time ago. As a result, the repository paths have changed. When trying to update or install new software we will get errors from the default repositories. The solution is to update the sources list to point to the archived repositories.

## Update the sources to point to the archived repositories

If we check our current sources for Debian 5 we get the following:

```console
cat /etc/apt/sources.list

deb http://ftp.us.debian.org/debian/ lenny main contrib non-free
deb http://http.us.debian.org/debian stable main contrib non-free
deb http://security.debian.org lenny/updates main contrib non-free
deb http://www.backports.org/debian lenny-backports main contrib non-free
deb http://10.82.108.51/kedars/sheevaplug_wifi/builds/packages/ binary/
```

We should replace the repository paths with the archived ones:

```console
deb http://archive.debian.org/debian/ lenny main contrib non-free
```

Then we can update and upgrade our distro:

```console
sudo apt-get update
sudo apt-get upgrade
```


If we get errors related to authentication and keys because of outdated credentials we can do the following:

## Troubleshoot

### Manually add keys

Some packages may have expired keys, which are necessary for the OS to verify their authenticity. We can manually add the missing keys to our OS keyring:

```console
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <KEY_ID-THAT-IS-MISSING>
```

### Bypass authentication

If we still have problems with expired GPG keys we can bypass any security with `--allow-unauthenticated` flag:

```console
apt-get install {package} --allow-unauthenticated
```

## Related links
- https://stackoverflow.com/questions/29070471/gpg-error-http-archive-debian-org-lenny-updates-release-the-following-signat
- https://serverfault.com/questions/337278/debian-how-can-i-securely-get-debian-archive-keyring-so-that-i-can-do-an-apt-g