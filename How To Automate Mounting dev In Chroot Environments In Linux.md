原文地址：https://ostechnix.com/auto-mount-dev-in-chroot/





# How To Automate Mounting /dev In Chroot Environments In Linux



If you’re using `mmdebstrap` to create minimal Debian-based systems, you might find it annoying to manually mount and unmount the `/dev` directory every time you use the chroot. The good news is, there are ways to automate this process! In this guide, we’ll show you how to make your workflow more efficient by **automatically mounting `/dev`** when you enter the chroot environment and unmounting it when you exit.



## Why Automate Mounting `/dev`?

When you create a chroot environment, it doesn’t have access to the host system’s `/dev` directory by default. This can cause errors when running commands like `apt update` because programs need access to device files like `/dev/null`.

```
[...]
/usr/bin/apt-key: 95: cannot create /dev/null: Permission denied
/usr/bin/apt-key: 95: cannot create /dev/null: Permission denied
E: gpgv, gpgv2 or gpgv1 required for verification, but neither seems installed
Err:3 http://deb.debian.org/debian bookworm-updates InRelease
  gpgv, gpgv2 or gpgv1 required for verification, but neither seems installed
[...]
```

You can solve this issue by **[manually mounting `/dev`](https://ostechnix.com/troubleshooting-mmdebstrap/)** ([[Troubleshooting mmdebstrap]]) every time you use the chroot. But it is tedious and time-consuming. Automating this process saves you effort and makes your workflow smoother.

## Solution 1: Use systemd-nspawn to Automate Mounting /dev in a Chroot

**systemd-nspawn** is a command-line tool included in the systemd suite that allows you to create and run lightweight, isolated system containers on Linux systems. It provides a way to execute commands or even entire operating systems within a sandboxed environment.



The `systemd-nspawn` tool can automatically handle mounting `/dev` and other directories.



### Step 1: Install `systemd-nspawn`

On Debian-based systems, install it with:

```
sudo apt update
sudo apt install systemd-container
```

### Step 2: Enter the Chroot with `systemd-nspawn`

Create a chroot environment using mmdebstrap:

```
mmdebstrap --variant=minbase stable /tmp/debian-rootfs
```

Next, enter the chroot using command:

```
sudo systemd-nspawn -D /tmp/debian-rootfs
```

`systemd-nspawn` automatically mounts `/dev`, `/proc`, and `/sys` inside the chroot. When you exit the chroot, it automatically unmounts these directories.

## Solution 2: Use Chrootmnt Script to Automatically Mount and Unmount /dev in Chroot Environments

**[Chrootmnt](https://gist.github.com/ostechnix/7ca184e32caf6f4e2db8eab9dbeb8259)** is a Bash script to mount and unmount `/dev` inside a chroot environment, ensuring seamless device access and automatic cleanup for secure Linux system management.



**Key Features**

1. **Flexible Inputs:** Works with any chroot directory and command.
2. **Error Handling:** Prevents failures caused by missing directories or improper arguments.
3. **Automatic Cleanup:** Avoids leaving mounted resources if interrupted.
4. **Pseudo-Terminal Support:** Ensures compatibility with interactive tools like SSH, screen, and tmux.

Chrootmnt script is available in our **[OSTechNix GitHub Gist](https://gist.github.com/ostechnix)** page. You can freely download and modify it as you wish.

### Step 1: Create the Script

Save the following script as `chrootmnt.sh`:

```
#!/usr/bin/env bash

# ------------------------------------------------------------------
# Script Name:   chrootmnt.sh
# Description:   A Bash script to mount and unmount /dev 
#                inside a chroot environment
# Website:       https://gist.github.com/ostechnix
# Version:       1.0
# Usage:         ./chrootmnt.sh /path/to/chroot command args
# ------------------------------------------------------------------

# Validate input
if [ $# -lt 2 ]; then
  echo "Usage: $0 /path/to/chroot command [args...]"
  exit 1
fi

# Path to the chroot directory
CHROOT_DIR="$1"
shift  # Remove the first argument (chroot path)

# Ensure the chroot directory exists
if [ ! -d "$CHROOT_DIR" ]; then
  echo "Error: Chroot directory $CHROOT_DIR does not exist."
  exit 1
fi

# Mount /dev and /dev/pts
sudo mount --bind /dev "$CHROOT_DIR/dev"
sudo mount --bind /dev/pts "$CHROOT_DIR/dev/pts"

# Handle unmounting on exit
cleanup() {
  sudo umount "$CHROOT_DIR/dev/pts"
  sudo umount "$CHROOT_DIR/dev"
}
trap cleanup EXIT

# Enter the chroot
sudo chroot "$CHROOT_DIR" "$@"
```



Here is a step-by-step explanation of how the script works:

**1. Input Validation**

```
if [ $# -lt 2 ]; then
  echo "Usage: $0 /path/to/chroot command [args...]"
  exit 1
fi
```



- Ensures the user provides

   

  at least two arguments

  :

  1. The path to the chroot directory.
  2. A command (e.g., `/bin/bash`) to execute inside the chroot.

- If arguments are missing, it displays usage instructions and exits.

**2. Store Arguments**

```
CHROOT_DIR="$1"
shift  # Remove the first argument (chroot path)
```

- Stores the **chroot directory path** in `CHROOT_DIR`.

- Uses

   

  ```
  shift
  ```

   

  to remove this argument, leaving only the command and its optional arguments.

  - Example: If input is:

     

    ```
    ./chrootmnt.sh /tmp/debian-rootfs /bin/bash
    ```

    - `CHROOT_DIR` = `/tmp/debian-rootfs`
    - Remaining args (`/bin/bash`) are passed to `chroot`.

**3. Directory Check**

```
if [ ! -d "$CHROOT_DIR" ]; then
  echo "Error: Chroot directory $CHROOT_DIR does not exist."
  exit 1
fi
```

- Confirms the specified chroot directory exists.
- If the directory is missing, it prints an error and exits.

**4. Mount `/dev` and `/dev/pts`**

```
sudo mount --bind /dev "$CHROOT_DIR/dev"
sudo mount --bind /dev/pts "$CHROOT_DIR/dev/pts"
```

- Binds the host's `/dev` and `/dev/pts`

   

  inside the chroot.

  - `/dev`: Provides device files (e.g., `/dev/null`, `/dev/tty`).
  - `/dev/pts`: Supports pseudo-terminals (used by programs like SSH and screen).

- Ensures programs inside the chroot can access devices and terminals correctly.

**5. Cleanup Function**

```
cleanup() {
  sudo umount "$CHROOT_DIR/dev/pts"
  sudo umount "$CHROOT_DIR/dev"
}
trap cleanup EXIT
```

- **Defines a function** (`cleanup`) that unmounts `/dev` and `/dev/pts`.

- Registers this function to run

   

  automatically when the script exits

   

  (successful or error).

  - Prevents leaving stale mounts if something goes wrong.

**6. Enter the Chroot**

```
sudo chroot "$CHROOT_DIR" "$@"
```

- Uses the `chroot` command to switch to the specified root directory (`CHROOT_DIR`).

- Executes the command provided as additional arguments (

  ```
  $@
  ```

  ).

  - Example:

     

    ```
    ./chrootmnt.sh /tmp/debian-rootfs /bin/bash
    ```

    - Executes `/bin/bash` inside the chroot.



**7. Automatic Cleanup**

- When the

   

  ```
  chroot
  ```

   

  session ends (either normally or due to an error), the script automatically:

  1. Unmounts `/dev/pts`.
  2. Unmounts `/dev`.

### Step 2: Make the Script Executable

Run the following command to make the script executable:

```
chmod +x chrootmnt.sh
```

### Step 3: Use the Script

First, make sure you created the chroot environment:

```
mmdebstrap --variant=minbase stable /tmp/debian-rootfs
```

Now, Instead of using `sudo chroot /tmp/debian-rootfs`, use the script to enter the chroot:

**Start a shell inside `/tmp/debian-rootfs`:**

```
./chrootmnt.sh /tmp/debian-rootfs /bin/bash
```

**Run a command (e.g., `ls -l /`) inside the chroot:**



```
./chrootmnt.sh /tmp/debian-rootfs ls -l /
```

Just make sure you have entered the correct path of your chroot environment. In this case, the chroot directory is `/tmp/debian-tootfs`. Replace this with your own.

## Which Solution Should You Use?

- **`systemd-nspawn`**: Best for advanced users who want a container-like experience.
- **Chrootmnt Script**: Best for simplicity and automation.

## Conclusion

Manually mounting and unmounting `/dev` every time you use the chroot is not productive. By using the `systemd-nspawn` or a wrapper script, you can automate this process and save time. Choose the method that best fits your workflow, and enjoy a smoother experience with `mmdebstrap`!
