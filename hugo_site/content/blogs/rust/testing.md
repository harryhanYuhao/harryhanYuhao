---
date: '2025-09-10T9:50:08+01:00'
draft: false
title: 'Rust Testing'
tags: ['rust', 'software-development', 'testing']
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: ""
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
---

Reproducible testing is important for reliable software development.
Rust has a powerful built-in testing features, so that test can be writting under the test modules, and invoked by `cargo test`.
For more details, see [rust doc](https://doc.rust-lang.org/book/ch11-01-writing-tests.html).
This blogs will focus on some convenient use cases.

## How to Write Tests.

```rs
fn plus_one(x: i32) -> i32 {
    x + 1
}

fn main() {
}

#[cfg(test)]
mod tests{
    #[test]
    fn it_works() {
        assert_eq!(2, super::plus_one(1));
    }
}
```

And fire the test with `cargo test`.

Note `println!` will not print anything in `cargo test`. 
In the case when test by printing is favourable, run 

```sh
cargo test -- --nocapture  # -- denotes the beginning of flags
```

Sometimes there may be thousands of tests in a crate. 
Passing arguments to `cargo test <args>` tells cargo to only run test functions whose name contains `<args>`. 
Note, the name of any parent module is also part of the name of the test function. (The above test fuction has name `test::it_works`.)

```sh
cargo test works  # only run test function whose name contains works.
```
