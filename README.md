# YouTube Music Player

A lightweight command-line music player for Linux using [mpv](https://mpv.io/) and [yt-dlp](https://github.com/yt-dlp/yt-dlp).

The goal is simple: play music from YouTube without keeping a full browser window open, reducing memory usage while working.

## Features

* Continuously play random YouTube videos or playlists
* Play a specific URL
* Toggle play/pause for the active player
* Control playback with KDE media keys through MPRIS
* Save YouTube videos and playlists to a local library
* Add and remove URLs from the command line
* List saved URLs
* Edit the music library
* Ignore comments and empty lines
* Uses `mpv` with video disabled
* Lightweight and terminal-friendly

## Requirements

* Linux
* Bash
* [mpv](https://mpv.io/)
* [yt-dlp](https://github.com/yt-dlp/yt-dlp)
* [socat](http://www.dest-unreach.org/socat/) for `music --pause`
* `mpv-mpris` for KDE media-key integration (optional)

### Ubuntu / Debian

Install the dependencies:

```bash
sudo apt install mpv yt-dlp socat mpv-mpris
```

For the latest version of `yt-dlp`, see the [official releases](https://github.com/yt-dlp/yt-dlp/releases).

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/youtube-music-player.git
cd youtube-music-player
```

Make the script executable:

```bash
chmod +x music
```

You can run it directly from the project directory:

```bash
./music
```

### Install the command

To make `music` available globally:

```bash
mkdir -p ~/.local/bin
cp music ~/.local/bin/music
chmod +x ~/.local/bin/music
```

Make sure `~/.local/bin` is in your `PATH`:

```bash
echo $PATH
```

If necessary:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

You should now be able to run:

```bash
music
```

from any directory.

## Usage

### Play a random URL

Run:

```bash
music
```

The player randomly selects a URL from the music library. When playback ends, it
selects another URL and continues playing. With more than one saved URL, it
will not select the same URL twice in a row.

### Play a specific URL

```bash
music "https://www.youtube.com/watch?v=XXXXXXXX"
```

Playlists are supported. Once the supplied URL or playlist finishes, playback
continues with a random URL from the music library:

```bash
music "https://www.youtube.com/playlist?list=XXXXXXXX"
```

### Add a URL

```bash
music --add "https://www.youtube.com/watch?v=XXXXXXXX"
```

Short form:

```bash
music -a "https://www.youtube.com/watch?v=XXXXXXXX"
```

Duplicate URLs are automatically ignored.

### Toggle play/pause

With music already playing, toggle pause or resume from any terminal:

```bash
music --pause
```

Short form:

```bash
music -p
```

### Stop playback

Press `Ctrl+C` once in the terminal running `music` to stop playback completely.

### KDE media keys

Install `mpv-mpris` to make `music` appear in KDE's standard media controller.
After starting `music`, the keyboard Play/Pause button controls it globally, just
like a browser media session. Restart `music` after installing the package.

### List saved URLs

```bash
music --list
```

Short form:

```bash
music -l
```

### Remove a URL

```bash
music --remove "https://www.youtube.com/watch?v=XXXXXXXX"
```

Short form:

```bash
music -r "https://www.youtube.com/watch?v=XXXXXXXX"
```

### Edit the music library

```bash
music --edit
```

This opens the music library using the editor defined by `$EDITOR`.

If no editor is configured, `nano` is used.

### Show help

```bash
music --help
```

## Music Library

The default music library is:

```text
~/.config/music/music.txt
```

The file contains one URL per line:

```text
# Rock
https://www.youtube.com/playlist?list=XXXXXXXX

# Electronic
https://www.youtube.com/playlist?list=YYYYYYYY

# Individual tracks
https://www.youtube.com/watch?v=ZZZZZZZZ
```

Comments start with `#` and empty lines are ignored.

Individual videos and playlists can be mixed in the same file.

## Why mpv?

A web browser can consume a significant amount of memory when playing YouTube, especially when multiple tabs, extensions, and development tools are running.

This project uses:

```bash
mpv --no-video URL
```

This allows YouTube content to be played as audio without maintaining the full YouTube web application.

The result is a much lighter setup for computers with limited RAM.

## Configuration

The music library follows the XDG Base Directory specification.

By default:

```text
~/.config/music/music.txt
```

If `XDG_CONFIG_HOME` is defined, it will be used instead:

```text
$XDG_CONFIG_HOME/music/music.txt
```

## Commands

| Command              | Description            |
| -------------------- | ---------------------- |
| `music`              | Play random URLs continuously |
| `music URL`          | Play a URL, then continue randomly |
| `music --pause`      | Toggle play/pause in the active player |
| `music --list`       | List saved URLs        |
| `music --add URL`    | Add a URL              |
| `music --remove URL` | Remove a URL           |
| `music --edit`       | Edit the music library |
| `music --help`       | Show help              |

### Short Commands

| Short | Long       |
| ----- | ---------- |
| `-p`  | `--pause`  |
| `-l`  | `--list`   |
| `-a`  | `--add`    |
| `-r`  | `--remove` |
| `-e`  | `--edit`   |
| `-h`  | `--help`   |

## Project Structure

```text
youtube-music-player/
├── music
├── music.example.txt
├── README.md
├── .gitignore
└── LICENSE
```

## Privacy

The music library is stored locally on your computer.

Personal URLs should not be committed to the repository.

If you maintain a public repository, use `music.example.txt` for example URLs and keep your personal `music.txt` outside the repository.

## License

MIT License.

See [LICENSE](LICENSE) for details.
