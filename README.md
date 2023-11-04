<!-- Using xml to align the text centered and setting as title -->
<h1 align="center">btrfs-manager</h1>

<!-- Using xml to align the text centered and setting as subtitle -->
<h3 align="center">A simple application to manage btrfs snapshots</h3>


<!-- Table of contents using html -->

<h4 align="center">
    🚧  btrfs-manager 🚀 Under construction...  🚧
</h4>

<!--ts-->
   * [About](#about)
   * [Features](#features)
   * [How it Works](#how-it-works)
   * [How to use](#how-to-use)
      * [Snapshot Info](#snapshot-info)
      * [Prerequisites](#prerequisites)
      * [Running](#running)
   * [License](#license)
   * [Author](#author)

## About

This project is a simple application to manage btrfs snapshots. I created it because I didn't like relying on **Timeshift** which doesn't allow for none Ubuntu style of laying out the subvolume structure and **Snapper GUI** out-of-date. So I decided to create my own application to manage btrfs snapshots for my personal use.

## Features

- [] Create snapshots
- [] Delete snapshots
- [X] Take snapshots with apt/dpkg.
- [] Add snapshot to grub menu (ported for **btrfs-grub**).
- [] Restore snapshots.

## How it Works

Creating a snapshot is a simple process, just enter the `@subvolume` that you want to create a snapshot of and set the location where you want to save the snapshot. However, this requires you to manually enter this into your terminal. So I created a simple script that does this for you. The script is located in the `scripts` folder and is called `create_snapshot.sh`. This script takes two arguments, the first is the subvolume you want to create a snapshot of and the second is the location where you want to save the snapshot. The script will then create a snapshot of the subvolume and save it to the location you specified. The script will also create a file called `snapshot.info` in the location you specified. This file contains information about the snapshot, such as the date and time it was created, the subvolume it was created from, and the location it was saved to. This file is used by the application to display information about the snapshot.

### Snapshot Info

The `snapshot.info` well contain the following information: Name (hostname-date-time), subvolume the snapshot was created from life time (how long the snapshot well live before it is deleted), and the location the snapshot was saved to.

### Prerequisites

Before you begin, you will need to have the following tools installed on your system:

- [Git](https://git-scm.com/)
- [btrfs-progs](https://btrfs.wiki.kernel.org/index.php/Main_Page)

### Running

```bash
# Clone this repository
$ git clone https://github.com/MichaelSchaecher/btrfs-manager.git /usr/local/bin/btrfs-manager
```

CD into the directory `cd /usr/local/bin/btrfs-manager` where you cloned the repository and run the following command:

```bash
# Run the application
sudo make install
```

Several files will be copied to the following locations:

- `btrfs-manager.service`  -> `/usr/lib/systemd/system/`
- `btrfs-manager.timer`    -> `/usr/lib/systemd/system/`
- `btrfs-manager-cleanup.service` -> `/usr/lib/systemd/system/`
- `btrfs-manager-cleanup.timer`   -> `/usr/lib/systemd/system/`
- `btrfs-manager.conf`     -> `/etc/btrfs-manager.conf`
- `btrfs-manager`          -> `/usr/local/bin/`
- `btrfs-manager-cleanup`  -> `/usr/local/bin/`

The application will be installed to `/usr/local/bin/` and the configuration file will be installed to `/etc/btrfs-manager.conf`. The application will also be installed as a systemd service and timer. The service will be enabled and started automatically. The timer will be enabled and started automatically.

The configuration file contains the following settings is used to by both the **btrfs-manager** and **btrfs-manager-cleanup** scripts. If you want to change any of the settings, you can do so by editing the configuration file.

```bash
$EDITOR /etc/btrfs-manager.conf
```

| Setting | Description | Default |
| :--- | :--- | :--- |
| `SNAPSHOT_LOCATION` | The location where snapshots are saved. | `/.snapshots` |
| `SNAPSHOT_LIFETIME` | The lifetime of snapshots in days. | `5` (in Days) |
| `SNAPSHOT_PREFIX` | The prefix of the snapshot name. | `hostname-<path>` |
| `SNAPSHOT_FORMAT` | The date format of the snapshot name. | `%Y-%m-%d_%H%M-%S` |
| `SNAPSHOT_LIMIT` | The number of snapshots to keep. | `15` |

The rest of the settings are done with flags when running the application; both the **btrfs-manager** and **btrfs-manager-cleanup** scriptt.

| Flag | Description | application |
| :--- | :--- | :--- |
| `version` | Display version information. | **btrfs-manager** and **btrfs-manager-cleanup** |
| `help` | Display help message for stander commands and basic options. | **btrfs-manager** and **btrfs-manager-cleanup** |
| `delete` | Delete snapshots. | **btrfs-manager-cleanup** |
| `list` | List snapshots. | **btrfs-manager** |
| `create` | Create snapshots. | **btrfs-manager** |
| `restore` | Restore snapshots. | **btrfs-manager** |
| `add` | Add snapshots to grub menu (This command is ran with btrfs-manager.timer/service). | **btrfs-manager** |
| `-t`\|`--tag` | Add a tag to the snapshot.info file about the snapshot or use the tag to delete snapshots. | **btrfs-manager** and **btrfs-manager-cleanup** |
| `-s`\|`--subvolume` | The subvolume to create or snapshot to delete. | **btrfs-manager** and **btrfs-manager-cleanup** |
| `-n`\|`--skip` | Don't delete snapshots but only manually: will cause default btrfs-manager-cleanup to skip. | **btrfs-manager** |
| `-h`\|`--help` | Display help message for options flagged with stander commands. | **btrfs-manager** and **btrfs-manager-cleanup** |
| `-c`\|`--comment` | Add a comment to the snapshot.info file about the snapshot. | **btrfs-manager** and **btrfs-manager-cleanup** |
| `-l`\|`--lifetime` | The lifetime of snapshots in days (default 5 days). | **btrfs-manager** and **btrfs-manager-cleanup** |
| `-p`\|`--prefix` | The prefix of the snapshot name (default hostname-<path>_<date>_<time>) | **btrfs-manager** and **btrfs-manager-cleanup** |

## License

This project is under the license [MIT](./COPYING).

## Author

Made with ❤️ by [Michael Schaecher](https://blackstewie.com) 👋🏽
