# GeoIP-update

This is an **unofficial** script for downloading the MaxMind GeoIP (legacy) database from multiple supported sources.

By default, the script downloads the database from Miyuru's site to `/usr/share/GeoIP`. You can change the path and source by setting the `$GEOIP_DIR` and `$GEOIP_SOURCE` variables. See the documentation below for more details.

## Table of Contents

- [Data Sources](#data-sources)
- [Installation](#installation)
- [Usage](#usage)
  - [Use with a specified data source](#use-with-a-specified-data-source)
  - [Use without installation](#use-without-installation)
- [License](#license)

## Data Sources

`geoipupdate-legacy` utilizes two sources for the legacy GeoIP databases. Both sources use [MaxMind](https://www.maxmind.com/)'s [GeoLite2 databases](https://dev.maxmind.com/geoip/geoip2/geolite2/) as their data source and rely on the [sherpya/geolite2legacy](https://github.com/sherpya/geolite2legacy) project to convert the data from the **MaxMind DB File Format** to the legacy GeoIP format. For more details, visit their websites:

- Miyuru (<https://miyuru.lk/geoiplegacy>)
- Mailfud (<https://mailfud.org/geoip-legacy/>)

Miyuru is the default data source, as Mailfud appears to have a stricter rate limit. However, note that Miyuru's service may not support IPv4 all the time. If you encounter any connectivity issues with it, refer to the usage documentation and switch to another data source.

## Installation

Download the `geoipupdate` script to your `$PATH`, such as `/usr/bin/` or `/usr/local/bin/`, and set the script to be executable. For example:

Using `curl`:

```sh
sudo curl -Lo /usr/local/bin/geoipupdate https://github.com/PeterDaveHello/geoipupdate-legacy/raw/master/geoipupdate
sudo chmod +x /usr/local/bin/geoipupdate
```

Using `wget`:

```sh
sudo wget -O /usr/local/bin/geoipupdate https://github.com/PeterDaveHello/geoipupdate-legacy/raw/master/geoipupdate
sudo chmod +x /usr/local/bin/geoipupdate
```

You can also use `git` to clone the whole repository, and create a symbolic link in your `$PATH`, allowing you to easily update the script using git pull in the future:

```sh
git clone https://github.com/PeterDaveHello/geoipupdate-legacy
sudo ln -s $PWD/geoipupdate-legacy/geoipupdate /usr/local/bin/
```

## Usage

Since `/usr/share/GeoIP` is typically owned by root, you may need to use `sudo` for root permission:

```sh
sudo geoipupdate
```

To download the database to a different location, set the GEOIP_DIR variable:

```sh
GEOIP_DIR=/dev/shm/GeoIP_temp/ geoipupdate
```

### Use with a specified data source

As mentioned in the [Data Sources](#data-sources) section, multiple data sources are supported. To specify the desired source, set the `$GEOIP_SOURCE`variable with the value of the source name, *in lower case*. For example:

```sh
GEOIP_SOURCE=mailfud sudo -E geoipupdate
```

Note: `sudo` requires the `-E` or `--preserve-env=GEOIP_SOURCE` flag to preserve the variable for the commands it calls, otherwise `geoipupdate` won't know which source you'd like to use.

### Use without installation

It's possible to directly pipe the latest script to bash, but this can be risky. Use this method only when you understand the implications:

- Using wget with original URL

  ```sh
  wget -qO- https://github.com/PeterDaveHello/geoipupdate-legacy/raw/master/geoipupdate | sudo bash
  ```

- Using curl with shortened URL, specifying the update source as `mailfud`:

  ```sh
  curl -sSLo- https://git.io/geoipupdate | GEOIP_SOURCE=mailfud sudo -E bash
  ```

## License

GPL-2.0 (GNU GENERAL PUBLIC LICENSE Version 2)
