Memory alignment is an important concept in systems programming. In Rust, we can use the `#[repr(C)]` attribute and the
mem module to inspect and experiment with memory alignment. Here's an example to demonstrate alignment and padding in a
struct:

```rust, no_run
#use std::mem;
#
#[repr(C)]
struct Example {
    a: u8,  // 1 byte
    b: u32, // 4 bytes
    c: u16, // 2 bytes
}
#
#fn main() {
#    let example = Example { a: 1, b: 2, c: 3 };
#    
#    // Display the size and alignment of the struct
#    println!("Size of Example is {} bytes", mem::size_of::<Example>());
#    println!("Alignment of Example: {} bytes", mem::align_of::<Example>());
#
#    // Display offsets of individual fields
#    let base_address = &example as *const Example as usize;
#    let a_offset = &example.a as *const u8 as usize - base_address;
#    let b_offset = &example.b as *const u32 as usize - base_address;
#    let c_offset = &example.c as *const u16 as usize - base_address;
#
#    println!("Offset of a: {}", a_offset);
#    println!("Offset of b: {}", b_offset);
#    println!("Offset of c: {}", c_offset);
#}

```

    Size of Example is 12 bytes
    Alignment of Example: 4 bytes
    Offset of a: 0
    Offset of b: 4
    Offset of c: 8

This structure contains three fields with collective size of 7 bytes. However, the size of the struct is 12 bytes.

Alignment indicates the required alignment of the struct. It is defined by the largest field. In this case, the largest
field is `u32`, which requires 4-byte alignment.

```rust, no_run
#use std::mem;
#
#[repr(C)]
struct Example {
    b: u32, // 4 bytes 
    a: u8,  // 1 byte
    c: u16, // 2 bytes
}
#
#fn main() {
#    let example = Example { a: 1, b: 2, c: 3 };
#    
#    // Display the size and alignment of the struct
#    println!("Size of Example is {} bytes", mem::size_of::<Example>());
#    println!("Alignment of Example: {} bytes", mem::align_of::<Example>());
#
#    // Display offsets of individual fields
#    let base_address = &example as *const Example as usize;
#    let b_offset = &example.b as *const u32 as usize - base_address;
#    let a_offset = &example.a as *const u8 as usize - base_address;
#    let c_offset = &example.c as *const u16 as usize - base_address;
#
#    println!("Offset of b: {}", b_offset);
#    println!("Offset of a: {}", a_offset);
#    println!("Offset of c: {}", c_offset);
#}

```

    Size of Example is 8 bytes
    Alignment of Example: 4 bytes
    Offset of b: 0
    Offset of a: 4
    Offset of c: 6

```rust
use std::mem;

fn main() {
    let v: Vec<i32> = vec![1,2,3];
    
    // Display the size and alignment of the vector
    println!("Size of Vec<i32> is {} bytes", mem::size_of_val(&v));
    println!("Alignment of Vec<i32>: {} bytes", mem::align_of_val(&v));
}

```

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

## Details {#details-section}
This is the detailed explanation.

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

Empty line

