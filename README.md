# `mail-on-fail`

Send an (e)mail if running a command fails.

## Usage

```
Usage: mail-on-fail --mailto <email> [--name <name>] executable args...

--mailto : Output is sent to this email on failure
--name   : The name to use in the email subject.
           Will use $executable if omitted.
--script : executable is considered a bash script
           (for bash -c), not a filename.
--help | -h        : Show usage help

```

`mail-on-fail` assumes that this host has a working mail setup and that `mail` (from mailutils) works.

## Examples

E.g. these _will not_ send a mail (because exit code is 0):

    mail-on-fail --mailto me@example.com --name 'Test ok' true
    mail-on-fail --mailto me@example.com --name 'Test ok' --script "echo body"

But these _will_ send a mail (because exit code is != 0):

    mail-on-fail --mailto me@example.com --name 'Test fail' false
    mail-on-fail --mailto me@example.com --name 'Test fail' --script "echo body ; exit 1"

## TODO

* Check for `stderr` output in addition to exit code. This is a short, tiny
  script. So far it only tests the exit code of the program being run. But in
  the future, a likely improvement to be to treat `stdout` and `stderr`
  separately and treat any output on `stderr` as a failure that sends emails
  too. So expect that to get working at  some  point  (patches welcome!)
