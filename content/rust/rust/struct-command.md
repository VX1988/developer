---
title: Struct command
type: docs
---

```rust
use std::process::Command;

let output = if cfg!(target_os = "windows") {
    Command::new("cmd")
        .args(["/C", "echo hello"])
        .output()
        .expect("failed to execute process")
} else {
    Command::new("sh")
        .arg("-c")
        .arg("echo hello")
        .output()
        .expect("failed to execute process")
};

let hello = output.stdout;
```

# Reused to spawn multiple processes

```rs
// The builder methods change the command without needing to immediately spawn the process.

use std::process::Command;

let mut echo_hello = Command::new("sh");
echo_hello.arg("-c").arg("echo hello"); // reused to spawn multiple processes
let hello_1 = echo_hello.output().expect("failed to execute process");
let hello_2 = echo_hello.output().expect("failed to execute process");
```