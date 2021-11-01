[![Build](https://github.com/rbspy/read-process-memory/actions/workflows/build.yml/badge.svg)](https://github.com/rbspy/read-process-memory/actions/workflows/build.yml) [![Build status](https://api.cirrus-ci.com/github/rbspy/read-process-memory.svg)] [![crates.io](https://img.shields.io/crates/v/read-process-memory.svg)](https://crates.io/crates/read-process-memory) [![](https://docs.rs/read-process-memory/badge.svg)](https://docs.rs/read-process-memory) [![Coverage Status](https://coveralls.io/repos/github/rbspy/read-process-memory/badge.svg?branch=master)](https://coveralls.io/github/rbspy/read-process-memory?branch=master)

A crate to read memory from another process. Code originally taken from Julia Evans' excellent [rbspy](https://github.com/rbspy/rbspy/) project.

# Example

```rust, no_run
extern crate read_process_memory;

use std::convert::TryInto;
use std::io;
use read_process_memory::{Pid, ProcessHandle, CopyAddress, copy_address};

// Try to read `size` bytes at `address` from the process `pid`.
fn read_some_memory(pid: Pid, address: usize, size: usize) -> io::Result<()> {
    let handle: ProcessHandle = pid.try_into()?;
    let _bytes = copy_address(address, size, &handle)?;
    println!("Read {} bytes", size);
    Ok(())
}

fn main() {
    read_some_memory(123 as Pid, 0x100000, 100).unwrap();
}
```

# Documentation

[https://docs.rs/read-process-memory](https://docs.rs/read-process-memory)
