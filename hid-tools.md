# hid-tools

- hid-tools is a set of tools to interact with the kernel's HID subsystem.

- It can be run directly from the git repository or installed via `pip3 install hid-tools`.

## Installation

- The `hid-tools` repository does not need to be installed, all tools and kernel tests can be run straight from the git repository, for example the following commands clone the repository and run the `hid-recorder` tool.

    ```sh
    $ git clone https://gitlab.freedesktop.org/libevdev/hid-tools
    $ cd hid-tools
    $ sudo ./hid-recorder
    ```

- Where the tools need to be installed, it is recommended to use `pip`:

    ```sh
    $ sudo pip3 install
    ```

- This installs all tools into the system-wid Python path.

- hid-tools needs root access to the /dev/hidraw` nodes, an installation in the user-specific paths will not usually work without further commandline tweaking configuration.

- Removal of th etools works with `pip` as well:

    ```sh
    $ pip3 uninstall hid-tools
    ```

## Debugging tools for users

### hid-recorder

- `hid-recorder` prints the HID Report Descriptor from a `/dev/hidraw` device node and any HID reports coming from that device.

- The output format can be used with `hid-replay` for debugging.

- When run without any arguments, the tool prints a list of available devices.

> ```sh
> $ pip install click parse
> ```

    ```sh
    $ sudo ./hid-recorder
    ```

### hid-replay

- `hid-replay` takes the output from `hid-recorder` and replays it through a virtual HID device that looks exactly like the one recorded.

- `hid-replay` requires UHID support so make sure `pyudev` is installed.

> ```sh
> $ pip install pyroute2
> $ pip install libevdev
> $ pip install pyudev
> ```

```sh
$ sudo hid-replay recording-file.hid
```

### hid-decode

- `hid-decode` takes a HID Report Descriptor andprints a human-readable version of it.

- `hid-decode` takes binary report descriptors, strings of bytes, and other formats.

```sh
$ hid-decode /sys/class/input/event5/device/device/report_descriptor
```

## kernel tests

- The `hid-tools` repository containsa number of tests exercisingthekernel HID subsystem.

- Thetests are not part of the `pip3` moduleand mustbe run from thegitrepository.

- The most convenient invocation of the tests is by simply calling `pytest`.

- The test suite requires UHID support so make sure `pyudev` is installed.

> ##### Note
>
> - If your testing system is running X, please follow the steps below to letX drivers ignore uhid testdevices.
>
> - Otherwise, the X driver will recognize and handlethe test devices, which would interfacewith the kernel tests and running session.
>
> ```sh
> $ sudo cp tests/91-hid-tools-uhid-test.conf /etc/X11/xorg.conf.d
> ```
>
> - Restart your X server

> ```sh
> $ pip install pytest
> $ pip install pyyaml
> $ pip install attrs
> ```

```sh
$ sudo pytest
```

- See the`pytest` documentation for information on how to run a subset of tests.
