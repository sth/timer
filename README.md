# Simple notifications

Command line command to easily show a notification after a specified time

## Examples

    timer 15m Close bathroom window
    timer 3m30s Tea ready
    timer 11:30 Meeting

## Dependencies

`timer` uses

- Python3
- notify-send (optional)

On Ubuntu or Debian you would make sure those are available with

    sudo apt install python3 libnotify-bin

By default `notify-send` is used to display desktop notifications, but a
different notification program can be configured.

## Usage

### Parameters

The first parameter is parsed as a time value. This can be either:

- A time intervall, e.g. `15m` or `1h15m10s`.
  - `d`: days
  - `h`: hours
  - `m`, `min`, or no suffix: minutes
  - `s`: seconds
  - `ms`: milliseconds
- A fixed time, like `11:30` or `12:15:30`

Any further parameters are used as a notification message that is displayed once
the timer expires.

### Options

Additional options can be passed:

- `--quiet`, `-q`: Suppress the "sheduled at ..." message
- `--configfile=FILENAME`: Use a non-standard config file

## Configuration

A optional config file can be created in `/etc/timer.conf` or `~/.config/timer.conf`
to customize the notification that is shown when the timer expires. The config file
uses a [ini-file structure][py-ini] and expects the config options in a `[timer]`
section:
 
    [timer]
    text = [{time:%H:%M}] | {message}
    command = notify-send -u critical "{text}"

### command

The `command` option specifies the command that is used to display the
notification when the timer expires. The command can [use shell-like quotes][py-shlex].
Python [`format()`][py-format] is used to substitute a `text`
string, containing the timer message and a `time` datetime value containing
the time of the notification. The default is:

    [timer]
    command = notify-send -u critical "{text}"

### text

The `text` option can be used to adjust formatting of the timer message text.
Python's [`format()`][py-format] is used to substitute a `message` string
(the timer message specified on the command line when the timer was started)
and `time`, a Python datetime value of the notification time.
The default is:

    [timer]
    text = [{time:%H:%M}] | {message}


 [py-init]: https://docs.python.org/3/library/configparser.html#supported-ini-file-structure
 [py-shlex]: https://docs.python.org/3/library/shlex.html#shlex.split
 [py-format]: https://docs.python.org/3/library/functions.html#format
