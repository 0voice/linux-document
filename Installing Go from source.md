原文地址：https://go.dev/doc/install/source#introduction





# Installing Go from source

| Table of Contents                                            |                                                              |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| [Introduction](https://go.dev/doc/install/source#introduction)[Install Go compiler binaries for bootstrap](https://go.dev/doc/install/source#go14)[Bootstrap toolchain from binary release](https://go.dev/doc/install/source#bootstrapFromBinaryRelease)[Bootstrap toolchain from cross-compiled source](https://go.dev/doc/install/source#bootstrapFromCrosscompiledSource)[Bootstrap toolchain using gccgo](https://go.dev/doc/install/source#bootstrapFromGccgo)[Bootstrap toolchain from C source code](https://go.dev/doc/install/source#bootstrapFromSource)[Install Git, if needed](https://go.dev/doc/install/source#git)[(Optional) Install a C compiler](https://go.dev/doc/install/source#ccompiler)[Fetch the repository](https://go.dev/doc/install/source#fetch)[(Optional) Switch to the master branch](https://go.dev/doc/install/source#head) | [Install Go](https://go.dev/doc/install/source#install)[Testing your installation](https://go.dev/doc/install/source#testing)[Set up your work environment](https://go.dev/doc/install/source#gopath)[Install additional tools](https://go.dev/doc/install/source#tools)[Community resources](https://go.dev/doc/install/source#community)[Keeping up with releases](https://go.dev/doc/install/source#releases)[Optional environment variables](https://go.dev/doc/install/source#environment) |

This topic describes how to build and run Go from source code. To install with an installer, see [Download and install](https://go.dev/doc/install).

## Introduction[¶](https://go.dev/doc/install/source#introduction)

Go is an open source project, distributed under a [BSD-style license](https://go.dev/LICENSE). This document explains how to check out the sources, build them on your own machine, and run them.

Most users don't need to do this, and will instead install from precompiled binary packages as described in [Download and install](https://go.dev/doc/install), a much simpler process. If you want to help develop what goes into those precompiled packages, though, read on.

There are two official Go compiler toolchains. This document focuses on the `gc` Go compiler and tools. For information on how to work on `gccgo`, a more traditional compiler using the GCC back end, see [Setting up and using gccgo](https://go.dev/doc/install/gccgo).

The Go compilers support the following instruction sets:

- `amd64`, `386`

  The `x86` instruction set, 64- and 32-bit.

- `arm64`, `arm`

  The `ARM` instruction set, 64-bit (`AArch64`) and 32-bit.

- `loong64`

  The 64-bit LoongArch instruction set.

- `mips64`, `mips64le`, `mips`, `mipsle`

  The `MIPS` instruction set, big- and little-endian, 64- and 32-bit.

- `ppc64`, `ppc64le`

  The 64-bit PowerPC instruction set, big- and little-endian.

- `riscv64`

  The 64-bit RISC-V instruction set.

- `s390x`

  The IBM z/Architecture.

- `wasm`

  [WebAssembly](https://webassembly.org/).



The compilers can target the AIX, Android, DragonFly BSD, FreeBSD, Illumos, Linux, macOS/iOS (Darwin), NetBSD, OpenBSD, Plan 9, Solaris, and Windows operating systems (although not all operating systems support all architectures).

A list of ports which are considered "first class" is available at the [first class ports](https://go.dev/wiki/PortingPolicy#first-class-ports) wiki page.

The full set of supported combinations is listed in the discussion of [environment variables](https://go.dev/doc/install/source#environment) below.

See the Go Wiki MinimumRequirements page for the [overall system requirements](https://go.dev/wiki/MinimumRequirements).

## Install Go compiler binaries for bootstrap[¶](https://go.dev/doc/install/source#go14)

The Go toolchain is written in Go. To build it, you need a Go compiler installed. The scripts that do the initial build of the tools look for a "go" command in `$PATH`, so as long as you have Go installed in your system and configured in your `$PATH`, you are ready to build Go from source. Or if you prefer you can set `$GOROOT_BOOTSTRAP` to the root of a Go installation to use to build the new Go toolchain; `$GOROOT_BOOTSTRAP/bin/go` should be the go command to use.

The minimum version of Go required depends on the target version of Go:

- Go <= 1.4: a C toolchain.
- 1.5 <= Go <= 1.19: a Go 1.4 compiler.
- 1.20 <= Go <= 1.21: a Go 1.17 compiler.
- 1.22 <= Go <= 1.23: a Go 1.20 compiler.
- Going forward, Go version 1.N will require a Go 1.M compiler, where M is N-2 rounded down to an even number. Example: Go 1.24 and 1.25 require Go 1.22.

There are four possible ways to obtain a bootstrap toolchain:

- Download a recent binary release of Go.
- Cross-compile a toolchain using a system with a working Go installation.
- Use gccgo.
- Compile a toolchain from Go 1.4, the last Go release with a compiler written in C.

These approaches are detailed below.

### Bootstrap toolchain from binary release[¶](https://go.dev/doc/install/source#bootstrapFromBinaryRelease)

To use a binary release as a bootstrap toolchain, see [the downloads page](https://go.dev/dl/) or use any other packaged Go distribution meeting the minimum version requirements.

### Bootstrap toolchain from cross-compiled source[¶](https://go.dev/doc/install/source#bootstrapFromCrosscompiledSource)

To cross-compile a bootstrap toolchain from source, which is necessary on systems Go 1.4 did not target (for example, `linux/ppc64le`), install Go on a different system and run [bootstrap.bash](https://go.dev/src/bootstrap.bash).

When run as (for example)

```
$ GOOS=linux GOARCH=ppc64 ./bootstrap.bash
```

`bootstrap.bash` cross-compiles a toolchain for that `GOOS/GOARCH` combination, leaving the resulting tree in `../../go-${GOOS}-${GOARCH}-bootstrap`. That tree can be copied to a machine of the given target type and used as `GOROOT_BOOTSTRAP` to bootstrap a local build.

### Bootstrap toolchain using gccgo[¶](https://go.dev/doc/install/source#bootstrapFromGccgo)

To use gccgo as the bootstrap toolchain, you need to arrange for `$GOROOT_BOOTSTRAP/bin/go` to be the go tool that comes as part of gccgo 5. For example on Ubuntu Vivid:

```
$ sudo apt-get install gccgo-5
$ sudo update-alternatives --set go /usr/bin/go-5
$ GOROOT_BOOTSTRAP=/usr ./make.bash
```

### Bootstrap toolchain from C source code[¶](https://go.dev/doc/install/source#bootstrapFromSource)

To build a bootstrap toolchain from C source code, use either the git branch `release-branch.go1.4` or [go1.4-bootstrap-20171003.tar.gz](https://dl.google.com/go/go1.4-bootstrap-20171003.tar.gz), which contains the Go 1.4 source code plus accumulated fixes to keep the tools running on newer operating systems. (Go 1.4 was the last distribution in which the toolchain was written in C.) After unpacking the Go 1.4 source, `cd` to the `src` subdirectory, set `CGO_ENABLED=0` in the environment, and run `make.bash` (or, on Windows, `make.bat`).

Once the Go 1.4 source has been unpacked into your GOROOT_BOOTSTRAP directory, you must keep this git clone instance checked out to branch `release-branch.go1.4`. Specifically, do not attempt to reuse this git clone in the later step named "Fetch the repository." The go1.4 bootstrap toolchain **must be able** to properly traverse the go1.4 sources that it assumes are present under this repository root.

Note that Go 1.4 does not run on all systems that later versions of Go do. In particular, Go 1.4 does not support current versions of macOS. On such systems, the bootstrap toolchain must be obtained using one of the other methods.

## Install Git, if needed[¶](https://go.dev/doc/install/source#git)

To perform the next step you must have Git installed. (Check that you have a `git` command before proceeding.)

If you do not have a working Git installation, follow the instructions on the [Git downloads](https://git-scm.com/downloads) page.

## (Optional) Install a C compiler[¶](https://go.dev/doc/install/source#ccompiler)

To build a Go installation with `cgo` support, which permits Go programs to import C libraries, a C compiler such as `gcc` or `clang` must be installed first. Do this using whatever installation method is standard on the system.

To build without `cgo`, set the environment variable `CGO_ENABLED=0` before running `all.bash` or `make.bash`.

## Fetch the repository[¶](https://go.dev/doc/install/source#fetch)

Change to the directory where you intend to install Go, and make sure the `goroot` directory does not exist. Then clone the repository and check out the latest release tag or release branch (`go1.22.0`, or `release-branch.go1.22`, for example):

```
$ git clone https://go.googlesource.com/go goroot
$ cd goroot
$ git checkout <tag>
```

Where `<tag>` is the version string of the release.

Go will be installed in the directory where it is checked out. For example, if Go is checked out in `$HOME/goroot`, executables will be installed in `$HOME/goroot/bin`. The directory may have any name, but note that if Go is checked out in `$HOME/go`, it will conflict with the default location of `$GOPATH`. See [`GOPATH`](https://go.dev/doc/install/source#gopath) below.

Reminder: If you opted to also compile the bootstrap binaries from source (in an earlier section), you still need to `git clone` again at this point (to checkout the latest `<tag>`), because you must keep your go1.4 repository distinct.

## (Optional) Switch to the master branch[¶](https://go.dev/doc/install/source#head)

If you intend to modify the go source code, and [contribute your changes](https://go.dev/doc/contribute.html) to the project, then move your repository off the release tag, and onto the master (development) branch. Otherwise, skip this step.

```
$ git checkout master
```

## Install Go[¶](https://go.dev/doc/install/source#install)

To build the Go distribution, run

```
$ cd src
$ ./all.bash
```

(To build under Windows use `all.bat`.)

If all goes well, it will finish by printing output like:

```
ALL TESTS PASSED

---
Installed Go for linux/amd64 in /home/you/go.
Installed commands in /home/you/go/bin.
*** You need to add /home/you/go/bin to your $PATH. ***
```

where the details on the last few lines reflect the operating system, architecture, and root directory used during the install.

For more information about ways to control the build, see the discussion of [environment variables](https://go.dev/doc/install/source#environment) below. `all.bash` (or `all.bat`) runs important tests for Go, which can take more time than simply building Go. If you do not want to run the test suite use `make.bash` (or `make.bat`) instead.

## Testing your installation[¶](https://go.dev/doc/install/source#testing)

Check that Go is installed correctly by building a simple program.

Create a file named `hello.go` and put the following program in it:

```
package main

import "fmt"

func main() {
	fmt.Printf("hello, world\n")
}
```

Then run it with the `go` tool:

```
$ go run hello.go
hello, world
```

If you see the "hello, world" message then Go is installed correctly.

## Set up your work environment[¶](https://go.dev/doc/install/source#gopath)

You're almost done. You just need to do a little more setup.

[**How to Write Go Code**Learn how to set up and use the Go tools](https://go.dev/doc/code.html)

The [How to Write Go Code](https://go.dev/doc/code.html) document provides **essential setup instructions** for using the Go tools.

## Install additional tools[¶](https://go.dev/doc/install/source#tools)

The source code for several Go tools (including [gopls](https://pkg.go.dev/golang.org/x/tools/gopls)) is kept in [the golang.org/x/tools repository](https://golang.org/x/tools). To install one of the tools (`gopls` in this case):

```
$ go install golang.org/x/tools/gopls@latest
```

## Community resources[¶](https://go.dev/doc/install/source#community)

The usual community resources listed on the [help page](https://go.dev/help/) have active developers that can help you with problems with your installation or your development work. For those who wish to keep up to date, there is another mailing list, [golang-checkins](https://groups.google.com/group/golang-checkins), that receives a message summarizing each checkin to the Go repository.

Bugs can be reported using the [Go issue tracker](https://go.dev/issue/new).

## Keeping up with releases[¶](https://go.dev/doc/install/source#releases)

New releases are announced on the [golang-announce](https://groups.google.com/group/golang-announce) mailing list. Each announcement mentions the latest release tag, for instance, `go1.9`.

To update an existing tree to the latest release, you can run:

```
$ cd go/src
$ git fetch
$ git checkout <tag>
$ ./all.bash
```

Where `<tag>` is the version string of the release.

## Optional environment variables[¶](https://go.dev/doc/install/source#environment)

The Go compilation environment can be customized by environment variables. *None is required by the build*, but you may wish to set some to override the defaults.

- ```
  $GOROOT
  ```

  The root of the Go tree, often `$HOME/go1.X`. Its value is built into the tree when it is compiled, and defaults to the parent of the directory where `all.bash` was run. There is no need to set this unless you want to switch between multiple local copies of the repository.

- ```
  $GOROOT_FINAL
  ```

  The value assumed by installed binaries and scripts when `$GOROOT` is not set explicitly. It defaults to the value of `$GOROOT`. If you want to build the Go tree in one location but move it elsewhere after the build, set `$GOROOT_FINAL` to the eventual location.

- ```
  $GOPATH
  ```

  The directory where Go projects outside the Go distribution are typically checked out. For example, `golang.org/x/tools` might be checked out to `$GOPATH/src/golang.org/x/tools`. Executables outside the Go distribution are installed in `$GOPATH/bin` (or `$GOBIN`, if set). Modules are downloaded and cached in `$GOPATH/pkg/mod`.

  The default location of `$GOPATH` is `$HOME/go`, and it's not usually necessary to set `GOPATH` explicitly. However, if you have checked out the Go distribution to `$HOME/go`, you must set `GOPATH` to another location to avoid conflicts.

- ```
  $GOBIN
  ```

  The directory where executables outside the Go distribution are installed using the [go command](https://go.dev/cmd/go). For example, `go install golang.org/x/tools/gopls@latest` downloads, builds, and installs `$GOBIN/gopls`. By default, `$GOBIN` is `$GOPATH/bin` (or `$HOME/go/bin` if `GOPATH` is not set). After installing, you will want to add this directory to your `$PATH` so you can use installed tools.

  Note that the Go distribution's executables are installed in `$GOROOT/bin` (for executables invoked by people) or `$GOTOOLDIR` (for executables invoked by the go command; defaults to `$GOROOT/pkg/$GOOS_$GOARCH`) instead of `$GOBIN`.

- ```
  $GOOS
  ```

   

  and

   

  ```
  $GOARCH
  ```

  The name of the target operating system and compilation architecture. These default to the values of `$GOHOSTOS` and `$GOHOSTARCH` respectively (described below).

  Choices for `$GOOS` are `android`, `darwin`, `dragonfly`, `freebsd`, `illumos`, `ios`, `js`, `linux`, `netbsd`, `openbsd`, `plan9`, `solaris`, `wasip1`, and `windows`.

  Choices for `$GOARCH` are `amd64` (64-bit x86, the most mature port), `386` (32-bit x86), `arm` (32-bit ARM), `arm64` (64-bit ARM), `ppc64le` (PowerPC 64-bit, little-endian), `ppc64` (PowerPC 64-bit, big-endian), `mips64le` (MIPS 64-bit, little-endian), `mips64` (MIPS 64-bit, big-endian), `mipsle` (MIPS 32-bit, little-endian), `mips` (MIPS 32-bit, big-endian), `s390x` (IBM System z 64-bit, big-endian), and `wasm` (WebAssembly 32-bit).

  The valid combinations of `$GOOS` and `$GOARCH` are:

  |      | `$GOOS`     | `$GOARCH`  |
  | ---- | ----------- | ---------- |
  |      | `aix`       | `ppc64`    |
  |      | `android`   | `386`      |
  |      | `android`   | `amd64`    |
  |      | `android`   | `arm`      |
  |      | `android`   | `arm64`    |
  |      | `darwin`    | `amd64`    |
  |      | `darwin`    | `arm64`    |
  |      | `dragonfly` | `amd64`    |
  |      | `freebsd`   | `386`      |
  |      | `freebsd`   | `amd64`    |
  |      | `freebsd`   | `arm`      |
  |      | `illumos`   | `amd64`    |
  |      | `ios`       | `arm64`    |
  |      | `js`        | `wasm`     |
  |      | `linux`     | `386`      |
  |      | `linux`     | `amd64`    |
  |      | `linux`     | `arm`      |
  |      | `linux`     | `arm64`    |
  |      | `linux`     | `loong64`  |
  |      | `linux`     | `mips`     |
  |      | `linux`     | `mipsle`   |
  |      | `linux`     | `mips64`   |
  |      | `linux`     | `mips64le` |
  |      | `linux`     | `ppc64`    |
  |      | `linux`     | `ppc64le`  |
  |      | `linux`     | `riscv64`  |
  |      | `linux`     | `s390x`    |
  |      | `netbsd`    | `386`      |
  |      | `netbsd`    | `amd64`    |
  |      | `netbsd`    | `arm`      |
  |      | `openbsd`   | `386`      |
  |      | `openbsd`   | `amd64`    |
  |      | `openbsd`   | `arm`      |
  |      | `openbsd`   | `arm64`    |
  |      | `plan9`     | `386`      |
  |      | `plan9`     | `amd64`    |
  |      | `plan9`     | `arm`      |
  |      | `solaris`   | `amd64`    |
  |      | `wasip1`    | `wasm`     |
  |      | `windows`   | `386`      |
  |      | `windows`   | `amd64`    |
  |      | `windows`   | `arm`      |
  |      | `windows`   | `arm64`    |

- ```
  $GOHOSTOS
  ```

   

  and

   

  ```
  $GOHOSTARCH
  ```

  The name of the host operating system and compilation architecture. These default to the local system's operating system and architecture.

  Valid choices are the same as for `$GOOS` and `$GOARCH`, listed above. The specified values must be compatible with the local system. For example, you should not set `$GOHOSTARCH` to `arm` on an x86 system.

- ```
  $GO386
  ```

   

  (for

   

  ```
  386
  ```

   

  only, defaults to

   

  ```
  sse2
  ```

  )

  This variable controls how gc implements floating point computations.

  - `GO386=softfloat`: use software floating point operations; should support all x86 chips (Pentium MMX or later).
  - `GO386=sse2`: use SSE2 for floating point operations; has better performance but only available on Pentium 4/Opteron/Athlon 64 or later.

- ```
  $GOARM
  ```

   

  (for

   

  ```
  arm
  ```

   

  only; default is auto-detected if building on the target processor, 7 if not)

  This sets the ARM floating point co-processor architecture version the run-time should target. If you are compiling on the target system, its value will be auto-detected.

  - `GOARM=5`: use software floating point; when CPU doesn't have VFP co-processor
  - `GOARM=6`: use VFPv1 only; default if cross compiling; usually ARM11 or better cores (VFPv2 or better is also supported)
  - `GOARM=7`: use VFPv3; usually Cortex-A cores

  If in doubt, leave this variable unset, and adjust it if required when you first run the Go executable. The [GoARM](https://go.dev/wiki/GoArm) page on the [Go community wiki](https://go.dev/wiki) contains further details regarding Go's ARM support.

- ```
  $GOAMD64
  ```

   

  (for

   

  ```
  amd64
  ```

   

  only; default is

   

  ```
  v1
  ```

  )

  This sets the microarchitecture level for which to compile. Valid values are `v1` (default), `v2`, `v3`, `v4`. See [the Go wiki MinimumRequirements page](https://go.dev/wiki/MinimumRequirements#amd64) for more information.

- ```
  $GOMIPS
  ```

   

  (for

   

  ```
  mips
  ```

   

  and

   

  ```
  mipsle
  ```

   

  only)

  ```
  $GOMIPS64
  ```

   

  (for

   

  ```
  mips64
  ```

   

  and

   

  ```
  mips64le
  ```

   

  only)

  These variables set whether to use floating point instructions. Set to "`hardfloat`" to use floating point instructions; this is the default. Set to "`softfloat`" to use soft floating point.

- ```
  $GOPPC64
  ```

   

  (for

   

  ```
  ppc64
  ```

   

  and

   

  ```
  ppc64le
  ```

   

  only)

  This variable sets the processor level (i.e. Instruction Set Architecture version) for which the compiler will target. The default is `power8`.

  - `GOPPC64=power8`: generate ISA v2.07 instructions
  - `GOPPC64=power9`: generate ISA v3.00 instructions

- ```
  $GORISCV64
  ```

   

  (for

   

  ```
  riscv64
  ```

   

  only)

  This variable sets the RISC-V user-mode application profile for which to compile. The default is `rva20u64`.

  - `GORISCV64=rva20u64`: only use RISC-V extensions that are mandatory in the [RVA20U64](https://github.com/riscv/riscv-profiles/blob/main/src/profiles.adoc#51-rva20u64-profile) profile
  - `GORISCV64=rva22u64`: only use RISC-V extensions that are mandatory in the [RVA22U64](https://github.com/riscv/riscv-profiles/blob/main/src/profiles.adoc#rva22u64-profile) profile

- ```
  $GOWASM
  ```

   

  (for

   

  ```
  wasm
  ```

   

  only)

  This variable is a comma separated list of [experimental WebAssembly features](https://github.com/WebAssembly/proposals) that the compiled WebAssembly binary is allowed to use. The default is to use no experimental features.

  - `GOWASM=satconv`: generate [saturating (non-trapping) float-to-int conversions](https://github.com/WebAssembly/nontrapping-float-to-int-conversions/blob/master/proposals/nontrapping-float-to-int-conversion/Overview.md)
  - `GOWASM=signext`: generate [sign-extension operators](https://github.com/WebAssembly/sign-extension-ops/blob/master/proposals/sign-extension-ops/Overview.md)

Note that `$GOARCH` and `$GOOS` identify the *target* environment, not the environment you are running on. In effect, you are always cross-compiling. By architecture, we mean the kind of binaries that the target environment can run: an x86-64 system running a 32-bit-only operating system must set `GOARCH` to `386`, not `amd64`.

If you choose to override the defaults, set these variables in your shell profile (`$HOME/.bashrc`, `$HOME/.profile`, or equivalent). The settings might look something like this:

```
export GOARCH=amd64
export GOOS=linux
```

although, to reiterate, none of these variables needs to be set to build, install, and develop the Go tree.
