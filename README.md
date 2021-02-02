# GeoIP-update

**Unofficial** script to download MaxMind GeoIP(legacy) database from multiple supported sources.

By default, it'll download the database from Miyuru's site to `/usr/share/GeoIP`, you can change the path and source by variable `$GEOIP_DIR` and `$GEOIP_SOURCE`, see the document below for more details.

## Table of Contents

- [Data source](#data-source)
- [Installation](#installation)
- [Usage](#usage)
  - [Use with specified data source](#use-with-specified-data-source)
  - [Use without installation](#use-without-installation)
- [License](#license)

## Data source

`geoipupdate-legacy` uses two sources of the legacy GeoIP databses, they are both using [MaxMind](https://www.maxmind.com/)'s [GeoLite2 databases](https://dev.maxmind.com/geoip/geoip2/geolite2/) as the data source, and using project [sherpya/geolite2legacy](https://github.com/sherpya/geolite2legacy) to convert the data from **MaxMind DB File Format** to the legacy GeoIp format we need. You can visit their websites for more details:

- Miyuru(<https://miyuru.lk/geoiplegacy>)
- mailfud(<https://mailfud.org/geoip-legacy/>)

Miyuru is currently the default data source, because mailfud seems to have more strict rate limit, but please be noted that Miyuru's service may not support IPv4 all the time, if you have any connectivity issue with it, see the usage document and switch to another data source.

## Installation

Download `geoipupdate` script to your `$PATH`, like `/usr/bin/` or `/usr/local/bin/`, and set the script to be executable, for example:

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

You can also use `git` to clone the whole repository, and use symbolic link in `$PATH`, so that you can simply update the script by `git pull` in the future:

```sh
git clone https://github.com/PeterDaveHello/geoipupdate-legacy
sudo ln -s $PWD/geoipupdate-legacy/geoipupdate /usr/local/bin/
```

## Usage

As by default, `/usr/share/GeoIP` is usually owned by root, you could use `sudo` for the root permission:

```sh
sudo geoipupdate
```

If you want to download the database to elsewhere, set the `GEOIP_DIR` variable:

```sh
GEOIP_DIR=/dev/shm/GeoIP_temp/ geoipupdate
```

### Use with specified data source

As we mention above in the [data source](#data-source) section, we support multiple data sources, you just need to specify the one you want to use, by setting `GEOIP_SOURCE` variable with the value of the source name, *in lower case*, for example:

```sh
GEOIP_SOURCE=mailfud sudo -E geoipupdate
```

Note: `sudo` needs `-E` or `--preserve-env=GEOIP_SOURCE` to preserve the variable for the commands it calls, otherwise `geoipupdate` won't be able to know which source you'd like to use.

### Use without installation

Directly pipe the latest script to bash is possible, but it's sometimes dangerous, use it only when you know what you're doing:

```sh
wget -qO- https://github.com/PeterDaveHello/geoipupdate-legacy/raw/master/geoipupdate | sudo bash
```

## License

GPL-2.0 (GNU GENERAL PUBLIC LICENSE Version 2)
