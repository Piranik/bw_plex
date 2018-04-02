# bw_plex
[![Travis Status](https://travis-ci.org/Hellowlol/bw_plex.svg?branch=master)](https://travis-ci.org/Hellowlol/bw_plex)
[![Cov](https://codecov.io/gh/hellowlol/bw_plex/branch/master/graph/badge.svg)](https://codecov.io/gh/hellowlol/bw_plex/branch/master)
[![GitHub Releases](https://img.shields.io/github/tag/hellowlol/bw_plex.svg?label=github+release)](https://github.com/hellowlol/bw_plex/releases)
[![PyPI version](https://badge.fury.io/py/bw_plex.svg)](https://pypi.python.org/pypi/bw_plex)
[![Code Health](https://landscape.io/github/Hellowlol/bw_plex/master/landscape.svg?style=flat)](https://landscape.io/github/Hellowlol/bw_plex/master)
[![Github commits (since latest release)](https://img.shields.io/github/commits-since/Hellowlol/bw_plex/latest.svg)](https://github.com/Hellowlol/bw_plex/compare)


binge watching for plex

## Install
You should install this from github as this project isnt stable.
```pip install -e git+https://github.com/Hellowlol/bw_plex.git#egg=bw_plex```
You should also install a speedup for the websocket-client package. ```pip install wsaccel```


## Usage
CPU/Memory usage can be rather high, so use a 64 bit python install.
Note: This tool only works on your local network.

```
Usage: bw_plex [OPTIONS] COMMAND [ARGS]...

  CLI tool that monitors pms and jumps the client to after the theme.

Options:
  -d, --debug             Add debug logging.
  -u, --username TEXT     Your plex username
  -p, --password TEXT     Your plex password
  -s, --servername TEXT   The server you want to monitor.
  --url TEXT              url to the server you want to monitor
  -t, --token TEXT        plex-x-token
  -c, --config TEXT       Not in use atm.
  -vs, --verify_ssl TEXT  Enable this to allow insecure connections to PMS
  --help                  Show this message and exit.

Commands:
  add_theme_to_hashtable  Create a hashtable from the themes.
  check_db                Do a manual check of the db.
  export_db               Test command for myself.
  ffmpeg_process          Simple manual test for ffmpeg_process with...
  find_theme              Iterate over all your shows and downloads the...
  manually_correct_theme  Set the correct fingerprint of the show in...
  match                   Manual match for a file.
  process                 Manual process some/all eps.
  set_manual_theme_time   Set a manual start and end time for a theme.
  watch                   Start watching the server for stuff to do.
```

The most common will be:
```bw_plex watch```

## How it works:

Bw_plex listens for playing events using websocket. We download the first 10 minutes of that episode and the theme music from YouTube.

We then create a audio print from the theme song that we match against the audio of the 10 minutes of the episode. (There’s a backup method that uses audio silence in combination with black frames too).

We then check if this episode has a recap using subtitles and audio where we look for clues like last season, previously on (add you own words in the config)

Depending on your settings we will then allow playback until the theme start or just jump straight to intro end if we also should skip recaps.

Since this is a rather slow process we also start processing the next episode so next time you watch the same show we instantly seek the client to the end of the theme.



