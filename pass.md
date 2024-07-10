# Pass

> the standard unix password manager

## Introducing `pass`

- Password management should be simple and follow Unix philosophy.

- With `pass`, each password lives inside of a `gpg` encrypted file whose filename is the title of the website or resource that requires the password.

- These encrypted files may be organized into meaningful folder hierarchies, copied from computer to computer, and, in general, manipulated using standard command line file management utilities.

- All passwords live in `~/.password-store`, and `pass` provides some nice commands for adding, editing, generating, and retrieving passwords.

- It is a very short and simple shell script.

- It's capable of temporarily putting passwords on your clipboard and tracking password changes using `git`.

- You can edit the password store using ordinary unix shell commands alongside the `pass` command.

- There is bash completion so that youcan simply hit tab to fill innames and commands.

- The very active community has produced many impressive clients and GUIs for otherplatforms as well as extensions for `pass` itself.

- The`pass` command is extensively documented in its man page.

### Using the password store

- We can list all the existing passwords in the store:

    ```sh
    $ pass
    ```

- And we can show passwords too:

    ```sh
    $ pass Email/zx2c4.com
    ```

- Or copy them to the clipboard:

    ```sh
    $ pass -c Email/zx2c4.com
    ```

- There will be a nice password input dialog using the standard `gpg-agent` (which can be configured to stay authenticated for several minutes), since all passwords are encrypted.

- We can add existing passwords to the store with `insert`:

    ```sh
    $ pass insert Business/cheese-whiz-factory
    ```

- This also handles multiline passwords or other data with `--multiline` or `-m`, and passwords can be edited in your default text editor using  `pass edit pass-name`.

- The utility can `generate` new passwords using `/dev/urandom` internally:

    ```sh
    $ pass generate Email/jasondonenfeld.com 15
    ```

- It's possible to generate passwords with no symbols using `--no-symbols` or `-n`, and we can copy it to the clipboard instead of displaying it at the console using `--clip` or `-c`.

- And of course, passwords can be removed:

    ```sh
    $ pass rm Business/cheese-whiz-factory
    ```

- If the password store is a git repository, since each manipulation creates a git commit, you can synchronize the password store using `pass git push` and `pass git pull`, which call `git-push` or `git-pull` on the store.

- You can read more examples and more features in the man page.

### Setting it up

- To begin, there is a single command to initialize the password store:

    ```sh
    $ pass init "ZX2C4 Password Storage Key"
    ```

- Here, `ZX2C4 Password Storage Key` is the ID of my GPG key.

- You can use your standard GPG key or use an alternative one especially for the password store as shown above.

- Multiple GPG keys can be specified, for using pass in a team setting, and different folders can have different GPG keys, by using `-p`.

- We can additionally initialize the password store as a git repository:

    ```sh
    $ pass git init
    $ pass git remote add origin kexec.com:pass-store
    ```

- If a git repository is initialized, `pass` create a git commit each time the password store is manipulated.

- There is a more detailed initialization example in the man page.

## Download

- The latest version is 1.7.4.

### Arch

```sh
# pacman -S pass
```

## Data Organization

### Usernames, Passwords, PINs, Websites, Metadata, et cetera

- The passwords store does not impose any particular schema or type of organization of your  data as it is simply a flat text file, which can contain arbitrary data.

- One approach is to use the multi-line functionality of pass (`--multiline` or `-m` in `insert`), and store the password itself on the first line of the file, and the additional information on subsequent lines.

- For example, `Amazon/bookreader` might look like this:

```
Yw|ZSNH!}z"6{ym9pI
URL: *.amazon.com/*
Username: AmazonianChicken@example.com
Secret Question 1: What is your childhood best friend's most bizarre superhero fantasy? Oh god, Amazon, it's too awful to say...
Phone Support PIN #: 84719
```

- *This is the preferred organizational scheme used by the author.*

- The `--clip`/ `-c` options will only copy the first line of such a file to the clipboard, thereby making it easy to fetch the password for login forms, while retaining additional information in the same file.

- Another approach is to use folders, and store each piece of data inside a file in that folder.

- And yet another approach might be to store the password in `Amazon/bookreader` and theadditional data in`Amazon/bookreader.meta`.

- And even another approach might be use multiline, as outlined above, but put the URL template in the filename instead of inside the file.

### Extensions for `pass`

- Extensions installed to `/usr/lib/password-store/extensions`(or some distro-specific variety of such) are always enabled.

- Extensions installed to `~/.password-store/.extensions/COMMAND.bash` are enabled if the `PASSWORD_STORE_ENABLE_EXTENSIONS` environment variable is `true`.

- Read the man page for more details.

- The community has produced many such extentions.

### Compatible Clients

- The community has assembled an impressive list of clients and GUIs for various platforms:

    - passmenu: an **extremely useful and awesome** dmenu script
