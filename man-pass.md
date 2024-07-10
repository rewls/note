# `man pass`

## Name

- pass - stores, retrieves, generates, and synchronizes passwords securely

## Synopsis

```sh
pass [ COMMAND ] [ OPTIONS ]... [ ARGS ]...
```

## Description

- `pass` is a very simple password store that keeps passwords inside `gpg2(1)` encrypted files inside a simple directory tree residing at `~/.password-store`.

- If no COMMAND is specified, COMMAND defaults to either `show` or `ls`, depending on the type of specifier in ARGS. 

## Commands

### `init gpg-id...`

- Initialize new password storage and use `gpg-id` for encryption.

- Multiple gpg-ids may be specified, in order to encrypt each password with multiple ids.

- This command must be run first before a password store can be used.

- If the specified gpg-id is different from the key used in any existing files, these files will be reencrypted to use the new id.

- Note that use of `gpg-agent(1)` is recommended so that the batch decryption does not require as much user intervention.

### `ls subfolder`

- List names of passwords inside the tree at subfolder by using the `tree(1)` program.

- This command is alternatively named `list`.

### `grep [GREPOPTIONS] search-string`

- Searches inside each decrypted password file for search-string, and displays line containing matched string along with filename.

- Uses `grep(1)` for matching.

- `GREPOPTIONS` are passed to `grep(1)` as-is.

### `find pass-names...`

- List names of passwords inside the tree that match `pass-names` by using the `tree(1)` program.

- This command is alternatively named `search`.

### `show [ --clip[=line-number], -c[line-number] ] [ --qrcode[=line-number], -q[line-number] ] pass-name`

- Decrypt and print a password named pass-name.

- If `--clip` or `-c` is specified, do not print the password but instead copy the first (or otherwise specified) line to the clipboard using `xclip(1)` or `wl-clipboard(1)` and the restore the clipboard after 45 (or `PASSWORD_STOTRE_CLIP_TIME`) seconds.

- If `--qrcode` or `-q` is specified, do not print the password but instead display a QR code using `qrencode(1)` either to the terminal or graphically if supported.

### `insert [ --echo, -e | --multiline, -m ] [ --force, -f ] pass-name`

- Insert a new password into the password store called `pass-name`.

- This will read the new password from standard in.

- If `--echo` or `-e` is not specified, disable keyboard echo when the password is entered and confirm the password by asking for it twice.

- If `--multiline` or `-m` specified, lines will be read until EOF or Ctrl+D is reached.

- Otherwise, only a single line from standard in is read.

- Prompt before overwriting an existing password, unless `--force` or `-f` is specified.

- This command is alternatively named `add`.

### `edit pass-name`

- Insert a new password or edit an existing password using the default text editor specified by the environment variable `EDITOR` or using `vi(1)` as a fallback.

- This mode makes use of temporary files for editin, but care is taken to ensure that temporary files are created in `/dev/shm` in order to avoid writing to difficult-to-erase disk sectors.

- If `/dev/shm` is not accessible, fallback to the ordinary `TMPDIR` location, and print a warning.

### `generate [ --no-symbols, -n ] [ --clip, -c ] [ --force -f ] pass-name [pass-length]`

- Generate a new password using `/dev/urandom` of length `pass-length` (or `PASSWORD_STORE_GENERATED_LENGTH` if unspecified) and insert into `pass-name.

- If `--no-symbols` or `-n` is specified, do not use any non-alphanumeric characters in the generated password.

- The character sets used in generating passwords can be changed with the `PASSWORD_STORE_CHARACTER_SET` and `PASSWORD_STORE_CHARACTER_SET_NO_SYMBOLS` environment variables, described below. 

### `rm [ --recursive, -r ] [ --force, -f ] pass-name`

- Remove the password named `pass-name` from the password store.

- This command is alternatively named `remove` or `delete`.

- If `--recursive` or `-r` is specified, delete pass-name recursively if it is a directory.

### `mv [ --force, -f ] old-path new-path

- Renames the password or directory named `old-path` to `new-path`.

- This command is alternatively named `rename`.

- If `new-path` ends in a trailing `/`, it is always treated as a directory.

### `cp [ --force, -f ] old-path new-path`

- Copies the password or directory named `old-path` to `new-path`.

- This command is alternatively named `copy`.

- If `new-path` ends in a trailing `/`, it is always treated as a directory.

### `git git-command-args...`

- If the password store is a git repository, pass `git-command-args` as arguments to `git(1)` using the password store as the git repository.

- If `git-command-args` is `init`, in addition to initializing the git repository, add the current contents of the password store to the repository in an initial commit.

### `help`

- Show usage message.

### `version`

- Show version information.

## Files

### `~/.password-store`

- The default password storage directory.

### `~/.password-store/.gpg-id`

- Contains the default gpg key identification used for encryption and decryption.

- Multiple gpg keys may be specified in this file, one per line.

- This should be set using the `init` command.

## Environment variables

### `PASSWORD_STORE_GENERATED_LENGTH`

- The default password length if the `pass-length` parameter  to `generate` is unspecified.

### `PASSWORD_STORE_CHARACTER_SET`

- The character set to be used in password generation for generate.

- This value is to be interpreted by `tr(1)`.

### `PASSWORD_STORE_CHARACTER_SET_NO_SYMBOLS`

- The character set to be used in no-symbol password generation for `generate`, when `--no-symbols`, `-n` is specified.

- This value is to be interpreted by `tr(1)`.

### `EDITOR`

- The location of the text editor used by `edit`.
