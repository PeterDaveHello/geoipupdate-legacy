# GeoIP-update

**Unofficial** script to download MaxMind GeoIP(legacy) database from <https://www.miyuru.lk/geoiplegacy>

By default, it'll download the database to `/usr/share/GeoIP`, you can change the path by variable `$GEOIP_DIR`.

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

## License

GPL-2.0 (GNU GENERAL PUBLIC LICENSE Version 2)
