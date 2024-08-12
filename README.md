![alt text](https://opnsense.org/wp-content/themes/OPNsense/assets/img/opnsense.png "Logo Title Text 1")

# OPNsense documentation

Welcome to the OPNsense documentation & wiki.   
The purpose of this project is to provide OPNsense users with quality documentation.

## Contribute

You can contribute to the project in many ways, e.g. testing
functionality, sending in bug reports or creating pull requests
directly via GitHub.  Any help is always very welcome!

## License

OPNsense documentation is available under the 2-Clause BSD license:

http://opensource.org/licenses/BSD-2-Clause

Every contribution made to the project must be licensed under the
same conditions in order to keep OPNsense truly free and accessible
for everybody.

Some pictures are licensed under the Creative Commons Zero (CC0) license:

https://creativecommons.org/publicdomain/zero/1.0/

Logos may be subject to additional copyrights, property
rights, trademarks etc. and may require the consent of a third party or the
license of these rights. Deciso B.V. does not represent or make any warranties
that it owns or licenses any of the mentioned, nor does it grant them.

#### Prepare build

On FreeBSD the following packages are required:

```
pkg install py39-pip jpeg-turbo gmake
```

Install Sphinx, our default theme and contrib packages:

```
pip[3] install -r requirements.txt --upgrade
```

### Update API endpoints

A script is provided to update the api endpoint documentation, this can be
executed using:

```
./collect_api_endpoints.py --repo core /path/to/core/repository
./collect_api_endpoints.py --repo plugins /path/to/plugins/repository
```

#### Generate HTML documents

```
make html
```

(```make clean``` to flush)

#### Live preview of HTML documents

Use `sphinx-autobuild` to track `source` for changes and get a live preview served via ``http://localhost:8000``.

```
pip[3] install sphinx-autobuild
```

```
sphinx-autobuild source build/html
```

#### Publish BIOS ROM Images

BIOS ROM images are written to OPNsense appliances using a FAT32 formatted drive containing in its root directory
the combined contents of the `source/hardware/files/BIOS_update_sources.zip` file and the latest platform-specific
compressed BIOS ROM image. The BIOS_update_sources directory contains the EFI boot structure to trigger the
`startup.nsh` file when booting from the drive.

```
0cf1b042223482ea073a7a3599d6170be7c849ff8399936cf5a9db1ec5406dcf  BIOS_update_sources.zip
```

Place a `.FD` ROM image into the `source/hardware/files/` directory and run:

```
./make_bios.py --platform <A10|A20|A30> --source <.FD filename>
```
