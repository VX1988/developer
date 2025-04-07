---
title: Random Stuffs
type: docs
prev: docs/rust/
weight: 3
---

`assert_eq!` is a macro used for testing and validation. It checks if two values are equal to each other, and if they are not, it will panic, causing the program to stop. This is commonly used in unit tests to ensure that the expected output matches the actual output.

`{:?}` It's a "debug" format specifier. When used with `{:?}`, the compiler will automatically choose the most appropriate way to display the given value.

`==` is padding in base64 format.

```bash
# Read Symbol Binary with readelf 
readelf -a <target binary>

# Check File size
ll <target binary>
```

```
ldd <- linux
dumpbin <- windows
```

A quick CTF-ish strings | grep is enough to find dependencies used in our target.

```bash
s=$(strings <binary sample path>); echo "${s//registry/\n}" | grep -a '\.rs' | sort
```

Creating a Python virtual environment in Linux

```bash
sudo apt-get install python-pip
pip install virtualenv
virtualenv --version
virtualenv <folder name>
virtualenv -p /usr/bin/python3 <folder name>
source rust-tool/bin/activate
deactivate (optional)
```

Unsued Rust disable warning

```rust
#![allow(unused)]
```

 `rustup show` : Some useful rustup commands
    
` rustup default <toolchain>` : Lists the installed toolchains ??
	
`rustup help` : Shows help for rustup

- Ref to decode base64 to vec: https://docs.rs/base64/0.22.1/base64/engine/trait.Engine.html#method.decode
