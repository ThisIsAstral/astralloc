# Simple C Allocator

A simple allocator for Linux, written in the C programming language.

## ⚠️ Disclaimer

I wrote this code for educational purposes while studying how memory allocators work. The code is very rough and is **not intended** for use in real, production-ready projects.

## ⚙️ How It Works

The allocator is based on the `mmap` and `mremap` system calls.

When you call `astralloc(1024)`, the following happens:

1.  The allocator determines the number of memory pages required for the requested size. For 1024 bytes, 4096 bytes will be allocated (the standard page size on Linux).
2.  It then saves information about the allocated block into a service structure and returns a pointer to the **allocated** memory.
3.  If there is remaining space in the allocated page, it will be used for subsequent allocations.
4.  When you use the allocator a second time and the requested amount of memory is smaller than the free remainder from the previous block, memory is allocated from this remainder.
5.  However, if the requested chunk is larger than the remainder, the existing region is expanded using `mremap`, "gluing" a new chunk to the old block while preserving all previous data.

## 📝 How to Use
**Allocating memory:**
```c
int* pointer_name = astralloc(size_in_bytes);
```
**Freeing all allocated memory:**
```c
aallocfree();
```
