---
title: Struct command
type: docs
---

```rust
use std::process::Command;

fn main() {
	if cfg!(target_os = "windows") {
		Command::new("cmd")
			.args(["/C", "echo hello"])
			.spawn()
			.expect("failed to execute process");
	} else {
		Command::new("sh")
			.arg("-c")
			.arg("echo hello")
			.output()
			.expect("failed to execute process");
	};
}

```

# Reused to spawn multiple processes

```rs
// Command can be reused to spawn multiple processes. The builder methods change the command without needing to immediately spawn the process.

use std::process::Command;

fn main() {
	let mut echo_hello = Command::new("cmd.exe");
	echo_hello.arg("/C").arg("echo hello");
	echo_hello.spawn().expect("failed to execute process");
	let hello_2 = echo_hello.status().expect("failed to execute process");
	let _ = echo_hello.output().expect("failed to execute process");
}

```
