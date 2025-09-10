---
title: Struct command
type: docs
---

```rs
// Unofficial Rust Internal
// std::sys::windows::process::Command

pub struct Command {
    program: OsString,
    args: Vec<Arg>,
    env: CommandEnv,
    cwd: Option<OsString>,
    flags: u32,
    detach: bool,
    stdin: Option<Stdio>,
    stdout: Option<Stdio>,
    stderr: Option<Stdio>,
    force_quotes_enabled: bool,
}
```

- `.spawn()` = ❌Not waits for process and ❌not capture output. (asynchronously)
- `.status()` = ✅Wait for process and ❌not capture output.
- `.output()` = ✅Wait for process and ✅capture output.


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

Command can be reused to spawn multiple processes. The builder methods change the command without needing to immediately spawn the process.

```rs

use std::process::Command;

fn main() {
	let mut echo_hello = Command::new("cmd.exe");
	echo_hello.arg("/C").arg("echo hello");
	echo_hello.spawn().expect("failed to execute process");
	let hello_2 = echo_hello.status().expect("failed to execute process");
	let _ = echo_hello.output().expect("failed to execute process");
}

```

Reuse and modify a Command object to spawn multiple processes with different settings.

```rs
use std::process::Command;

fn main() {
    let mut list_dir = Command::new("cmd");

    // Run `cmd /C dir` in the current directory
    list_dir.args(["/C", "dir"]);
    list_dir.status().expect("process failed to execute");

    println!();

    // Change to the root directory (C:\)
    list_dir.current_dir("C:\\"); // Change to the root directory (C:\)

    // Run `cmd /C dir` again, now in C:\
    list_dir.status().expect("process failed to execute");
}

```

# Scripting in strings.

- By doing this way, you no need to escape all `\` OR `, i waste a lot of time solving this and i find this approach is much more easier. PS is more flexibel when there is complex script, F cmd.

```rs
use std::process::{Command, Stdio};

fn main() {
    let _ = Command::new("powershell.exe")
        .arg("-ExecutionPolicy")
        .arg("Bypass")
        .arg("-Command")
        .arg(r#"Your script is here"#)
        .status()
        .unwrap();
}
```