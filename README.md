# Simple notifications

## Examples

    timer 15m Close bathroom window
    timer 3m30s Tea ready

## Dependencies

`timer` uses

- Python3
- notify-send (optional)

On Ubuntu or Debian you would make sure those are available with

    sudo apt install python3 libnotify-bin

By default `notify-send` is used to display desktop notifications, but a
different notification program can be configured.

## Configuration

A optional config file can be created in `/etc/timer.conf` or `~/.config/timer.conf`
to customize the notification that is shown when the timer expires. The config file
uses a [ini-file structure][py-ini] and expects the config options in a `[timer]`
section:
 
    [timer]
    notifycmd = notify-send -u critical "{notifytext}"
    notifytext = [{notifytime:%H:%M}] | {message}

### notifycmd

The `notifycmd` option specifies the command that is used to display the
notification when the timer expires. The command can [use shell-like quotes][py-shlex].
Python [`format()`][py-format] is used to substitute a `notifytext`
string, containing the timer message and a `notifytime` datetime value containing
the time of the notification. The default is:

    [timer]
	 notifycmd = notify-send -u critical "{notifytext}"

### notifytext

The `notifytext` option can be used to adjust formatting of the timer message text.
Python's [`format()`][py-format] is used to substitute a `message` string
(the timer message specified on the command line when the timer was started)
and `notifytime`, a Python datetime value of the notification time.
The default is:

    [timer]
    notifytext = [{notifytime:%H:%M}] | {message}


 [py-init]: https://docs.python.org/3/library/configparser.html#supported-ini-file-structure
 [py-shlex]: https://docs.python.org/3/library/shlex.html#shlex.split
 [py-format]: https://docs.python.org/3/library/functions.html#format
