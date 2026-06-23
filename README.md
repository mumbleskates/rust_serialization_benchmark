<!-- AUTOMATICALLY GENERATED, DO NOT EDIT -->
<!-- edit README.md.template instead -->

# Rust serialization benchmark

The goal of these benchmarks is to provide thorough and complete benchmarks for various rust
serialization frameworks.

## Maintainers

These benchmarks are maintained by a small group of volunteers. Special thanks to:

- [djkoloski](https://github.com/djkoloski)
- [mumbleskates](https://github.com/mumbleskates)
- [finnbear](https://github.com/finnbear)

## These benchmarks are a work in progress

These benchmarks are still being developed and pull requests to improve benchmarks are welcome.

## [Interactive site](https://djkoloski.github.io/rust_serialization_benchmark/)

Calculate the number of messages per second that can be sent/received with various rust serialization frameworks and compression libraries.
[Documentation](pages/README.md)

## Format

All tests benchmark the following properties (time or size):

* **Serialize**: serialize data into a buffer
* **Deserialize**: deserializes a buffer into a normal rust object
* **Borrow**: deserializes a buffer into a rust object that borrows string data from the input, with lifetime
* **Size**: the size of the buffer when serialized
* **Zlib**: the size of the buffer after zlib compression
* **Zstd**: the size of the buffer after zstd compression
* **Zstd Time**: the time taken to compress the serialized buffer with zstd

Zero-copy deserialization libraries have an additional set of benchmarks:

* **Access**: accesses a buffer as structured data
* **Read**: runs through a buffer and reads fields out of it
* **Update**: updates a buffer as structured data

Some benchmark results may be italicized and followed by an asterisk. Mouse over these for more details on what situation was benchmarked. Other footnotes are located at the bottom.

## Last updated: /dev/fd/63

<details><summary>Runtime info</summary>

### `rustc` version

```
rustc 1.98.0-nightly (f428d123a 2026-06-19)
binary: rustc
commit-hash: f428d123ab0ea5431ec4256ff8838b9342866446
commit-date: 2026-06-19
host: x86_64-unknown-linux-gnu
release: 1.98.0-nightly
LLVM version: 22.1.7
```

</details>

## `log`

This data set is composed of HTTP request logs that are small and contain many strings.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*436.07 µs\**</span> <span title="prepend">*418.64 µs\**</span> | 2.5423 ms | 866.82 µs | 804955 | 328941 | 284849 | 4.1837 ms |
| [bin-proto 0.12.7][bin-proto] | 4.1150 ms | 4.4883 ms | † | 1045784 | 373127 | 311553 | 4.4394 ms |
| [bincode 2.0.1][bincode] | 364.41 µs | 2.1310 ms | 687.70 µs | 741295 | 303944 | 256422 | 3.3461 ms |
| [bincode 1.3.3][bincode1] | 555.58 µs | 2.0729 ms | 640.53 µs | 1045784 | 373127 | 311553 | 4.3819 ms |
| [bitcode 0.6.6][bitcode] | 140.31 µs | 1.4634 ms | 60.507 µs | 703710 | 288826 | 227322 | 2.5263 ms |
| [borsh 1.5.7][borsh] | 550.58 µs | 2.1279 ms | † | 885780 | 362204 | 286248 | 4.0736 ms |
| capnp:<br> [capnp 0.23.2][capnp] | 501.63 µs <span title="packed">*1.4264 ms\**</span> | <span title="packed">*1.0084 ms\**</span> | † | 1443216 <span title="packed">*1046865\**</span> | 513986 <span title="packed">*481681\**</span> | 426532 <span title="packed">*458024\**</span> | 6.3298 ms <span title="packed">*5.2842 ms\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 609.61 µs | 5.2988 ms | 3.5193 ms | 1407835 | 403440 | 323561 | 4.9723 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.1541 ms | 11.256 ms | † | 1407835 | 403440 | 323561 | 4.9586 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.8836 ms | 4.7890 ms | 3.2211 ms | 1407835 | 403440 | 323561 | 4.6251 ms |
| [columnar 0.11.1][columnar] | 259.43 µs | 2.1666 ms <span title="copy_from">*823.92 µs\**</span> | † | 1045928 | 370212 | 293907 | 4.2166 ms |
| [compactly 0.1.6][compactly] | 27.194 ms | 20.178 ms | † | 241251 | 241453 | 241263 | 109.27 µs |
| [databuf 0.5.0][databuf] | 277.39 µs | 2.0317 ms | 665.80 µs | 765778 | 311715 | 263914 | 3.4625 ms |
| [dlhn 0.1.7][dlhn] | 660.75 µs | 2.5654 ms | † | 724953 | 301446 | 253056 | 3.1436 ms |
| [flatbuffers 25.12.19][flatbuffers] | 1.0410 ms | † | † | 1276368 | 468539 | 388381 | 4.7231 ms |
| [flexbuffers 25.2.10][flexbuffers] | 6.6079 ms | 7.3351 ms | 5.6047 ms | 1829756 | 714318 | 691541 | 8.7713 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.7728 ms | 3.9444 ms | † | 1827461 | 470560 | 360727 | 5.4709 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 3.6192 ms | 5.9290 ms | † | 1827461 | 470560 | 360727 | 5.9058 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.1321 ms | 4.7382 ms | † | 1827461 | 470560 | 360727 | 5.6202 ms |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 360.03 µs | 2.5665 ms | 938.27 µs | 764996 | 315291 | 264212 | 3.5665 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.5433 ms | 3.1737 ms | 1.4778 ms | 784997 | 325384 | 277608 | 3.6880 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 357.20 µs | 2.4889 ms | 811.13 µs | 784997 | 325384 | 277608 | 3.7239 ms |
| [minicbor 1.0.0][minicbor] | 500.92 µs | 3.0045 ms | 1.4056 ms | 817830 | 332671 | 284034 | 3.9345 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.3513 ms | 3.9995 ms | 2.4742 ms | 818669 | 332556 | 284797 | 3.9536 ms |
| [nanoserde 0.2.1][nanoserde] | 253.46 µs | 2.0979 ms | † | 1045784 | 373127 | 311553 | 4.2599 ms |
| [nibblecode 0.1.0][nibblecode] | 193.35 µs | † | † | 1011487 | 494573 | 429872 | 5.3416 ms |
| [postcard 1.1.1][postcard] | 431.21 µs | 2.2798 ms | 703.84 µs | 724953 | 302399 | 252968 | 3.2349 ms |
| [pot 3.0.1][pot] | 2.1980 ms | 6.4243 ms | 4.9491 ms | 971922 | 372513 | 303636 | 4.3728 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*957.19 µs\**</span> <span title="populate + encode">*2.4885 ms\**</span> | 3.4538 ms | † | 884628 | 363130 | 314959 | 4.3466 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.1914 ms\**</span> <span title="populate + encode">*3.0393 ms\**</span> | 3.9071 ms | † | 884628 | 363130 | 314959 | 4.3685 ms |
| [rkyv 0.8.10][rkyv] | 249.52 µs | <span title="unvalidated">*1.5492 ms\**</span> <span title="validated upfront with error">*1.8918 ms\**</span> | † | 1011488 | 393526 | 325965 | 4.5088 ms |
| [ron 0.10.1][ron] | 10.670 ms | 25.169 ms | 22.677 ms | 1607459 | 449158 | 349324 | 5.5866 ms |
| [savefile 0.18.6][savefile] | 196.27 µs | 2.0790 ms | † | 1045800 | 373139 | 311562 | 4.3054 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 648.91 µs | 2.3217 ms | † | 765778 | 311743 | 263822 | 3.4483 ms |
| [serde-brief 0.1.1][serde-brief] | 1.4110 ms | 4.6295 ms | 2.9842 ms | 1584946 | 413733 | 339964 | 4.8814 ms |
| [serde_bare 0.5.0][serde_bare] | 691.22 µs | 2.1351 ms | † | 765778 | 311715 | 263914 | 3.5169 ms |
| [speedy 0.8.7][speedy] | 198.55 µs | 1.7553 ms | 375.80 µs | 885780 | 362204 | 286248 | 3.8088 ms |
| [wincode 0.5.3][wincode] | 172.52 µs | 1.7637 ms | 381.96 µs | 1045784 | 373127 | 311553 | 4.0937 ms |
| [wiring 0.2.4][wiring] | 198.17 µs | 2.0621 ms | † | 1045784 | 337930 | 275808 | 3.7452 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*72.911 ns\**</span> | <span title="validated on-demand with error">*132.49 µs\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 23.360 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4912 ns\**</span> <span title="validated upfront with error">*2.0767 ms\**</span> | <span title="unvalidated">*51.546 µs\**</span> <span title="validated upfront with error">*2.1597 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2447 ns\**</span> <span title="validated upfront with error">*236.84 µs\**</span> | <span title="unvalidated">*10.502 µs\**</span> <span title="validated upfront with error">*247.55 µs\**</span> | <span title="unvalidated">*7.5786 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2449 ns\**</span> <span title="validated upfront with error">*348.95 µs\**</span> | <span title="unvalidated">*10.412 µs\**</span> <span title="validated upfront with error">*357.95 µs\**</span> | <span title="unvalidated">*7.6665 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*32.18%\**</span> <span title="prepend">*33.52%\**</span> | 32.41% | 6.98% | 29.97% | 73.40% | 79.80% | 2.61% |
| [bin-proto 0.12.7][bin-proto] | 3.41% | 18.36% | † | 23.07% | 64.71% | 72.96% | 2.46% |
| [bincode 2.0.1][bincode] | 38.50% | 38.66% | 8.80% | 32.54% | 79.44% | 88.65% | 3.27% |
| [bincode 1.3.3][bincode1] | 25.25% | 39.75% | 9.45% | 23.07% | 64.71% | 72.96% | 2.49% |
| [bitcode 0.6.6][bitcode] | 100.00% | 56.30% | 100.00% | 34.28% | 83.60% | 100.00% | 4.33% |
| [borsh 1.5.7][borsh] | 25.48% | 38.72% | † | 27.24% | 66.66% | 79.41% | 2.68% |
| capnp:<br> [capnp 0.23.2][capnp] | 27.97% <span title="packed">*9.84%\**</span> | <span title="packed">*81.71%\**</span> | † | 16.72% <span title="packed">*23.05%\**</span> | 46.98% <span title="packed">*50.13%\**</span> | 53.30% <span title="packed">*49.63%\**</span> | 1.73% <span title="packed">*2.07%\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 23.02% | 15.55% | 1.72% | 17.14% | 59.85% | 70.26% | 2.20% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 4.45% | 7.32% | † | 17.14% | 59.85% | 70.26% | 2.20% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 7.45% | 17.20% | 1.88% | 17.14% | 59.85% | 70.26% | 2.36% |
| [columnar 0.11.1][columnar] | 54.08% | 38.03% <span title="copy_from">*100.00%\**</span> | † | 23.07% | 65.22% | 77.34% | 2.59% |
| [compactly 0.1.6][compactly] | 0.52% | 4.08% | † | 100.00% | 100.00% | 94.22% | 100.00% |
| [databuf 0.5.0][databuf] | 50.58% | 40.55% | 9.09% | 31.50% | 77.46% | 86.13% | 3.16% |
| [dlhn 0.1.7][dlhn] | 21.23% | 32.12% | † | 33.28% | 80.10% | 89.83% | 3.48% |
| [flatbuffers 25.12.19][flatbuffers] | 13.48% | † | † | 18.90% | 51.53% | 58.53% | 2.31% |
| [flexbuffers 25.2.10][flexbuffers] | 2.12% | 11.23% | 1.08% | 13.18% | 33.80% | 32.87% | 1.25% |
| json:<br> [flexon 0.4.5][flexon] | 5.06% | 20.89% | † | 13.20% | 51.31% | 63.02% | 2.00% |
| json:<br> [serde_json 1.0.140][serde_json] | 3.88% | 13.90% | † | 13.20% | 51.31% | 63.02% | 1.85% |
| json:<br> [simd-json 0.15.1][simd-json] | 6.58% | 17.39% | † | 13.20% | 51.31% | 63.02% | 1.94% |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 38.97% | 32.10% | 6.45% | 31.54% | 76.58% | 86.04% | 3.06% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 9.09% | 25.96% | 4.09% | 30.73% | 74.21% | 81.89% | 2.96% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 39.28% | 33.10% | 7.46% | 30.73% | 74.21% | 81.89% | 2.93% |
| [minicbor 1.0.0][minicbor] | 28.01% | 27.42% | 4.30% | 29.50% | 72.58% | 80.03% | 2.78% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.62% | 20.60% | 2.45% | 29.47% | 72.61% | 79.82% | 2.76% |
| [nanoserde 0.2.1][nanoserde] | 55.36% | 39.27% | † | 23.07% | 64.71% | 72.96% | 2.57% |
| [nibblecode 0.1.0][nibblecode] | 72.57% | † | † | 23.85% | 48.82% | 52.88% | 2.05% |
| [postcard 1.1.1][postcard] | 32.54% | 36.14% | 8.60% | 33.28% | 79.85% | 89.86% | 3.38% |
| [pot 3.0.1][pot] | 6.38% | 12.83% | 1.22% | 24.82% | 64.82% | 74.87% | 2.50% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*14.66%\**</span> <span title="populate + encode">*5.64%\**</span> | 23.86% | † | 27.27% | 66.49% | 72.18% | 2.51% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*11.78%\**</span> <span title="populate + encode">*4.62%\**</span> | 21.09% | † | 27.27% | 66.49% | 72.18% | 2.50% |
| [rkyv 0.8.10][rkyv] | 56.23% | <span title="unvalidated">*53.18%\**</span> <span title="validated upfront with error">*43.55%\**</span> | † | 23.85% | 61.36% | 69.74% | 2.42% |
| [ron 0.10.1][ron] | 1.31% | 3.27% | 0.27% | 15.01% | 53.76% | 65.07% | 1.96% |
| [savefile 0.18.6][savefile] | 71.49% | 39.63% | † | 23.07% | 64.71% | 72.96% | 2.54% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 21.62% | 35.49% | † | 31.50% | 77.45% | 86.16% | 3.17% |
| [serde-brief 0.1.1][serde-brief] | 9.94% | 17.80% | 2.03% | 15.22% | 58.36% | 66.87% | 2.24% |
| [serde_bare 0.5.0][serde_bare] | 20.30% | 38.59% | † | 31.50% | 77.46% | 86.13% | 3.11% |
| [speedy 0.8.7][speedy] | 70.67% | 46.94% | 16.10% | 27.24% | 66.66% | 79.41% | 2.87% |
| [wincode 0.5.3][wincode] | 81.33% | 46.72% | 15.84% | 23.07% | 64.71% | 72.96% | 2.67% |
| [wiring 0.2.4][wiring] | 70.80% | 39.96% | † | 23.07% | 71.45% | 82.42% | 2.92% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.71%\**</span> | <span title="validated on-demand with error">*7.86%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 5.33% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.96%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*20.20%\**</span> <span title="validated upfront with error">*0.48%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.14%\**</span> <span title="validated upfront with error">*4.21%\**</span> | <span title="unvalidated">*100.00%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.98%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*2.91%\**</span> | <span title="unvalidated">*98.85%\**</span> |

## `mesh`

This data set is a single mesh. The mesh contains an array of triangles, each of which has three vertices and a normal vector.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*7.3228 ms\**</span> <span title="prepend">*8.7194 ms\**</span> | 7.6934 ms | 8625005 | 6443961 | 6231572 | 75.993 ms |
| [bin-proto 0.12.7][bin-proto] | 8.2867 ms | 6.1877 ms | 6000008 | 5378500 | 5346908 | 8.5306 ms |
| [bincode 2.0.1][bincode] | 2.8882 ms | 1.0374 ms | 6000005 | 5378497 | 5346882 | 8.5502 ms |
| [bincode 1.3.3][bincode1] | 5.9133 ms | 5.7969 ms | 6000008 | 5378500 | 5346908 | 8.5186 ms |
| [bitcode 0.6.6][bitcode] | 1.3184 ms | 809.93 µs | 6000006 | 5182295 | 4921841 | 13.989 ms |
| [borsh 1.5.7][borsh] | 6.1957 ms | 4.3096 ms | 6000004 | 5378496 | 5346866 | 8.6576 ms |
| capnp:<br> [capnp 0.23.2][capnp] | 5.5288 ms <span title="packed">*16.522 ms\**</span> | <span title="packed">*13.203 ms\**</span> | 14000088 <span title="packed">*10401737\**</span> | 7130367 <span title="packed">*7308001\**</span> | 6046182 <span title="packed">*7922110\**</span> | 84.321 ms <span title="packed">*66.916 ms\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 9.1933 ms | 47.983 ms | 13125016 | 7524114 | 6757437 | 95.084 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 65.965 ms | 111.31 ms | 13122324 | 7524660 | 6759128 | 95.224 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 34.838 ms | 41.707 ms | 13122324 | 7524660 | 6759128 | 93.478 ms |
| [columnar 0.11.1][columnar] | 1.7792 ms | 1.4406 ms <span title="copy_from">*709.62 µs\**</span> | 6000120 | 5378435 | 5347039 | 8.5579 ms |
| [compactly 0.1.6][compactly] | 354.89 ms | 281.84 ms | 4846786 | 4850065 | 4846903 | 1.7558 ms |
| [databuf 0.5.0][databuf] | 2.4171 ms | 5.4049 ms | 6000003 | 5378495 | 5346897 | 8.7779 ms |
| [dlhn 0.1.7][dlhn] | 5.9389 ms | 6.7397 ms | 6000003 | 5378495 | 5346897 | 8.8260 ms |
| [flatbuffers 25.12.19][flatbuffers] | 516.55 µs | † | 6000024 | 5378434 | 5346878 | 8.9734 ms |
| [flexbuffers 25.2.10][flexbuffers] | 103.01 ms | 77.852 ms | 26609424 | 11901040 | 12486322 | 151.56 ms |
| json:<br> [flexon 0.4.5][flexon] | 77.267 ms | 54.922 ms | 26192883 | 9566084 | 8584671 | 157.66 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 88.173 ms | 100.50 ms | 26192883 | 9566084 | 8584671 | 158.60 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 53.938 ms | 66.382 ms | 26192883 | 9566084 | 8584671 | 158.74 ms |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 655.23 µs | 5.0083 ms | 7500005 | 6058442 | 6014500 | 10.318 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 20.327 ms | 16.452 ms | 8125006 | 6494876 | 6391037 | 70.635 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 756.97 µs | 5.2364 ms | 8125006 | 6494876 | 6391037 | 71.286 ms |
| [minicbor 1.0.0][minicbor] | 5.1950 ms | 11.401 ms | 8125006 | 6494907 | 6390894 | 69.230 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 116.80 ms | 25.882 ms | 8125037 | 6493484 | 6386940 | 70.981 ms |
| [nanoserde 0.2.1][nanoserde] | 1.7629 ms | 828.55 µs | 6000008 | 5378500 | 5346908 | 8.6721 ms |
| [nibblecode 0.1.0][nibblecode] | 200.79 µs | † | 6000008 | 5378500 | 5346908 | 8.7521 ms |
| [postcard 1.1.1][postcard] | 480.11 µs | 1.1074 ms | 6000003 | 5378495 | 5346897 | 8.9369 ms |
| [pot 3.0.1][pot] | 39.649 ms | 69.512 ms | 10122342 | 6814618 | 6852252 | 82.780 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*7.7937 ms\**</span> <span title="populate + encode">*8.6431 ms\**</span> | 14.855 ms | 8750000 | 6665735 | 6421877 | 72.643 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*14.622 ms\**</span> <span title="populate + encode">*24.137 ms\**</span> | 24.230 ms | 8750000 | 6665735 | 6421877 | 73.817 ms |
| [rkyv 0.8.10][rkyv] | 205.58 µs | <span title="unvalidated">*202.20 µs\**</span> <span title="validated upfront with error">*202.06 µs\**</span> | 6000008 | 5378500 | 5346872 | 8.5409 ms |
| [ron 0.10.1][ron] | 174.02 ms | 531.85 ms | 22192885 | 8970395 | 8137334 | 154.45 ms |
| [savefile 0.18.6][savefile] | 149.29 µs | 149.65 µs | 6000024 | 5378519 | 5346896 | 8.6069 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 5.1620 ms | 4.0100 ms | 6000004 | 5378496 | 5346866 | 8.5897 ms |
| [serde-brief 0.1.1][serde-brief] | 17.219 ms | 36.221 ms | 15750015 | 8024540 | 6813667 | 100.25 ms |
| [serde_bare 0.5.0][serde_bare] | 6.0100 ms | 4.5966 ms | 6000003 | 5378495 | 5346897 | 8.7010 ms |
| [speedy 0.8.7][speedy] | 149.14 µs | 149.18 µs | 6000004 | 5378496 | 5346866 | 8.5244 ms |
| [wincode 0.5.3][wincode] | 149.95 µs | 148.86 µs | 6000008 | 5378500 | 5346908 | 8.7180 ms |
| [wiring 0.2.4][wiring] | 151.04 µs | 338.30 µs | 6000008 | 5378952 | 5346905 | 8.7931 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*104.73 ns\**</span> | <span title="validated on-demand with error">*1.9871 ms\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 21.797 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4906 ns\**</span> <span title="validated upfront with error">*45.834 ns\**</span> | <span title="unvalidated">*77.861 µs\**</span> <span title="validated upfront with error">*77.928 µs\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2451 ns\**</span> <span title="validated upfront with error">*1.5572 ns\**</span> | <span title="unvalidated">*39.071 µs\**</span> <span title="validated upfront with error">*38.934 µs\**</span> | <span title="unvalidated">*100.14 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2450 ns\**</span> <span title="validated upfront with error">*5.3076 ns\**</span> | <span title="unvalidated">*38.917 µs\**</span> <span title="validated upfront with error">*38.925 µs\**</span> | <span title="unvalidated">*100.43 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*2.04%\**</span> <span title="prepend">*1.71%\**</span> | 1.93% | 56.19% | 75.27% | 77.78% | 2.31% |
| [bin-proto 0.12.7][bin-proto] | 1.80% | 2.41% | 80.78% | 90.18% | 90.65% | 20.58% |
| [bincode 2.0.1][bincode] | 5.16% | 14.35% | 80.78% | 90.18% | 90.65% | 20.54% |
| [bincode 1.3.3][bincode1] | 2.52% | 2.57% | 80.78% | 90.18% | 90.65% | 20.61% |
| [bitcode 0.6.6][bitcode] | 11.31% | 18.38% | 80.78% | 93.59% | 98.48% | 12.55% |
| [borsh 1.5.7][borsh] | 2.41% | 3.45% | 80.78% | 90.18% | 90.65% | 20.28% |
| capnp:<br> [capnp 0.23.2][capnp] | 2.70% <span title="packed">*0.90%\**</span> | <span title="packed">*1.13%\**</span> | 34.62% <span title="packed">*46.60%\**</span> | 68.02% <span title="packed">*66.37%\**</span> | 80.16% <span title="packed">*61.18%\**</span> | 2.08% <span title="packed">*2.62%\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 1.62% | 0.31% | 36.93% | 64.46% | 71.73% | 1.85% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 0.23% | 0.13% | 36.94% | 64.46% | 71.71% | 1.84% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 0.43% | 0.36% | 36.94% | 64.46% | 71.71% | 1.88% |
| [columnar 0.11.1][columnar] | 8.38% | 10.33% <span title="copy_from">*20.98%\**</span> | 80.78% | 90.18% | 90.65% | 20.52% |
| [compactly 0.1.6][compactly] | 0.04% | 0.05% | 100.00% | 100.00% | 100.00% | 100.00% |
| [databuf 0.5.0][databuf] | 6.17% | 2.75% | 80.78% | 90.18% | 90.65% | 20.00% |
| [dlhn 0.1.7][dlhn] | 2.51% | 2.21% | 80.78% | 90.18% | 90.65% | 19.89% |
| [flatbuffers 25.12.19][flatbuffers] | 28.87% | † | 80.78% | 90.18% | 90.65% | 19.57% |
| [flexbuffers 25.2.10][flexbuffers] | 0.14% | 0.19% | 18.21% | 40.75% | 38.82% | 1.16% |
| json:<br> [flexon 0.4.5][flexon] | 0.19% | 0.27% | 18.50% | 50.70% | 56.46% | 1.11% |
| json:<br> [serde_json 1.0.140][serde_json] | 0.17% | 0.15% | 18.50% | 50.70% | 56.46% | 1.11% |
| json:<br> [simd-json 0.15.1][simd-json] | 0.28% | 0.22% | 18.50% | 50.70% | 56.46% | 1.11% |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 22.76% | 2.97% | 64.62% | 80.05% | 80.59% | 17.02% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 0.73% | 0.90% | 59.65% | 74.68% | 75.84% | 2.49% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 19.70% | 2.84% | 59.65% | 74.68% | 75.84% | 2.46% |
| [minicbor 1.0.0][minicbor] | 2.87% | 1.31% | 59.65% | 74.67% | 75.84% | 2.54% |
| [nachricht-serde 0.4.0][nachricht-serde] | 0.13% | 0.58% | 59.65% | 74.69% | 75.89% | 2.47% |
| [nanoserde 0.2.1][nanoserde] | 8.46% | 17.97% | 80.78% | 90.18% | 90.65% | 20.25% |
| [nibblecode 0.1.0][nibblecode] | 74.28% | † | 80.78% | 90.18% | 90.65% | 20.06% |
| [postcard 1.1.1][postcard] | 31.06% | 13.44% | 80.78% | 90.18% | 90.65% | 19.65% |
| [pot 3.0.1][pot] | 0.38% | 0.21% | 47.88% | 71.17% | 70.73% | 2.12% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.91%\**</span> <span title="populate + encode">*1.73%\**</span> | 1.00% | 55.39% | 72.76% | 75.47% | 2.42% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.02%\**</span> <span title="populate + encode">*0.62%\**</span> | 0.61% | 55.39% | 72.76% | 75.47% | 2.38% |
| [rkyv 0.8.10][rkyv] | 72.55% | <span title="unvalidated">*73.62%\**</span> <span title="validated upfront with error">*73.67%\**</span> | 80.78% | 90.18% | 90.65% | 20.56% |
| [ron 0.10.1][ron] | 0.09% | 0.03% | 21.84% | 54.07% | 59.56% | 1.14% |
| [savefile 0.18.6][savefile] | 99.90% | 99.47% | 80.78% | 90.17% | 90.65% | 20.40% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 2.89% | 3.71% | 80.78% | 90.18% | 90.65% | 20.44% |
| [serde-brief 0.1.1][serde-brief] | 0.87% | 0.41% | 30.77% | 60.44% | 71.14% | 1.75% |
| [serde_bare 0.5.0][serde_bare] | 2.48% | 3.24% | 80.78% | 90.18% | 90.65% | 20.18% |
| [speedy 0.8.7][speedy] | 100.00% | 99.79% | 80.78% | 90.18% | 90.65% | 20.60% |
| [wincode 0.5.3][wincode] | 99.46% | 100.00% | 80.78% | 90.18% | 90.65% | 20.14% |
| [wiring 0.2.4][wiring] | 98.74% | 44.00% | 80.78% | 90.17% | 90.65% | 19.97% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.19%\**</span> | <span title="validated on-demand with error">*1.96%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 5.71% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.99%\**</span> <span title="validated upfront with error">*2.72%\**</span> | <span title="unvalidated">*49.98%\**</span> <span title="validated upfront with error">*49.94%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*79.95%\**</span> | <span title="unvalidated">*99.61%\**</span> <span title="validated upfront with error">*99.96%\**</span> | <span title="unvalidated">*100.00%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*23.46%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*99.98%\**</span> | <span title="unvalidated">*99.71%\**</span> |

## `minecraft_savedata`

This data set is composed of Minecraft player saves that contain highly structured data.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*887.66 µs\**</span> <span title="prepend">*786.97 µs\**</span> | 3.1605 ms | 1.7414 ms | 489348 | 281173 | 249360 | 2.6818 ms |
| [bin-proto 0.12.7][bin-proto] | 1.8703 ms | 2.9214 ms | † | 566975 | 239350 | 231475 | 2.4547 ms |
| [bincode 2.0.1][bincode] | 350.44 µs | 1.8126 ms | 782.83 µs | 367413 | 221291 | 206242 | 2.0415 ms |
| [bincode 1.3.3][bincode1] | 595.59 µs | 1.8658 ms | 873.38 µs | 569975 | 240525 | 231884 | 2.4426 ms |
| [bitcode 0.6.6][bitcode] | 128.15 µs | 1.2714 ms | 172.06 µs | 327688 | 200947 | 182040 | 734.60 µs |
| [borsh 1.5.7][borsh] | 555.17 µs | 1.8136 ms | † | 446595 | 234236 | 209834 | 2.0595 ms |
| capnp:<br> [capnp 0.23.2][capnp] | 429.05 µs <span title="packed">*1.0220 ms\**</span> | <span title="packed">*572.54 µs\**</span> | † | 803896 <span title="packed">*489017\**</span> | 335606 <span title="packed">*293127\**</span> | 280744 <span title="packed">*271528\**</span> | 3.5362 ms <span title="packed">*2.5496 ms\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 747.06 µs | 4.7787 ms | 3.5058 ms | 1109831 | 344745 | 274333 | 3.4321 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.6945 ms | 9.8753 ms | † | 1109821 | 344751 | 274345 | 3.4134 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.8869 ms | 4.6518 ms | 3.4208 ms | 1109821 | 344751 | 274345 | 3.4646 ms |
| [columnar 0.11.1][columnar] | 292.80 µs | 1.8815 ms <span title="copy_from">*756.62 µs\**</span> | † | 563728 | 249696 | 217582 | 1.6039 ms |
| [compactly 0.1.6][compactly] | 11.627 ms | 11.280 ms | † | 149292 | 149433 | 149304 | 71.163 µs |
| [databuf 0.5.0][databuf] | 294.95 µs | 1.7348 ms | 780.33 µs | 356311 | 213062 | 198403 | 2.0323 ms |
| [dlhn 0.1.7][dlhn] | 694.16 µs | 2.7095 ms | † | 366496 | 220600 | 205586 | 2.0140 ms |
| [flatbuffers 25.12.19][flatbuffers] | 3.2807 ms | † | † | 849472 | 347816 | 294871 | 3.4687 ms |
| [flexbuffers 25.2.10][flexbuffers] | 7.7704 ms | 6.8176 ms | 5.5903 ms | 1187688 | 557642 | 553730 | 6.2215 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.6631 ms | 4.5403 ms | † | 1623191 | 466527 | 359157 | 5.6709 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 3.6764 ms | 6.9515 ms | † | 1623191 | 466527 | 359157 | 5.6887 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.2240 ms | 4.5434 ms | † | 1623191 | 466527 | 359157 | 5.8675 ms |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 327.04 µs | 2.8279 ms | 1.3355 ms | 391251 | 236877 | 220395 | 2.3584 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.5093 ms | 2.9957 ms | 1.7291 ms | 424533 | 245214 | 226077 | 2.2803 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 384.72 µs | 2.2272 ms | 924.45 µs | 416025 | 243812 | 224965 | 2.2738 ms |
| [minicbor 1.0.0][minicbor] | 584.24 µs | 3.3854 ms | 1.8717 ms | 428773 | 249857 | 228630 | 2.2386 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.0558 ms | 3.7832 ms | 2.6806 ms | 449745 | 252432 | 230965 | 2.3404 ms |
| [nanoserde 0.2.1][nanoserde] | 265.38 µs | 1.9066 ms | † | 567975 | 239930 | 231872 | 2.4382 ms |
| [nibblecode 0.1.0][nibblecode] | 176.65 µs | † | † | 603928 | 431766 | 408796 | 3.5748 ms |
| [postcard 1.1.1][postcard] | 449.40 µs | 2.0752 ms | 802.46 µs | 367489 | 221913 | 207244 | 2.0368 ms |
| [pot 3.0.1][pot] | 2.3802 ms | 6.0778 ms | 4.9000 ms | 599125 | 299158 | 247675 | 2.7556 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.2651 ms\**</span> <span title="populate + encode">*3.0249 ms\**</span> | 3.5832 ms | † | 596811 | 305319 | 268737 | 2.9655 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.0526 ms\**</span> <span title="populate + encode">*3.0141 ms\**</span> | 3.8211 ms | † | 596811 | 305319 | 268737 | 3.0148 ms |
| [rkyv 0.8.10][rkyv] | 327.78 µs | <span title="unvalidated">*1.5183 ms\**</span> <span title="validated upfront with error">*1.8659 ms\**</span> | † | 603776 | 254776 | 219421 | 2.3334 ms |
| [ron 0.10.1][ron] | 7.6050 ms | 25.552 ms | 23.644 ms | 1465223 | 434935 | 342907 | 5.6130 ms |
| [savefile 0.18.6][savefile] | 214.86 µs | 1.9048 ms | † | 566991 | 239362 | 231478 | 2.4476 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 614.59 µs | 2.0837 ms | † | 356311 | 212976 | 198423 | 1.9356 ms |
| [serde-brief 0.1.1][serde-brief] | 1.2243 ms | 5.1683 ms | 3.5233 ms | 1276014 | 373898 | 293384 | 3.6440 ms |
| [serde_bare 0.5.0][serde_bare] | 764.98 µs | 2.3703 ms | † | 356311 | 213062 | 198403 | 1.9703 ms |
| [speedy 0.8.7][speedy] | 268.99 µs | 1.7013 ms | 565.88 µs | 449595 | 234970 | 210192 | 2.1452 ms |
| [wincode 0.5.3][wincode] | 207.02 µs | 1.6424 ms | 562.56 µs | 566975 | 239350 | 231475 | 2.4881 ms |
| [wiring 0.2.4][wiring] | 205.91 µs | 1.9246 ms | † | 566975 | 247810 | 225086 | 2.5197 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*68.723 ns\**</span> | <span title="validated on-demand with error">*409.82 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 880.33 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4915 ns\**</span> <span title="validated upfront with error">*2.1693 ms\**</span> | <span title="unvalidated">*1.4200 µs\**</span> <span title="validated upfront with error">*2.1716 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2450 ns\**</span> <span title="validated upfront with error">*247.49 µs\**</span> | <span title="unvalidated">*156.24 ns\**</span> <span title="validated upfront with error">*245.69 µs\**</span> | <span title="unvalidated">*761.38 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2451 ns\**</span> <span title="validated upfront with error">*323.43 µs\**</span> | <span title="unvalidated">*156.34 ns\**</span> <span title="validated upfront with error">*330.15 µs\**</span> | <span title="unvalidated">*747.76 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*14.44%\**</span> <span title="prepend">*16.28%\**</span> | 18.12% | 9.88% | 30.51% | 53.15% | 59.87% | 2.65% |
| [bin-proto 0.12.7][bin-proto] | 6.85% | 19.60% | † | 26.33% | 62.43% | 64.50% | 2.90% |
| [bincode 2.0.1][bincode] | 36.57% | 31.59% | 21.98% | 40.63% | 67.53% | 72.39% | 3.49% |
| [bincode 1.3.3][bincode1] | 21.52% | 30.69% | 19.70% | 26.19% | 62.13% | 64.39% | 2.91% |
| [bitcode 0.6.6][bitcode] | 100.00% | 45.03% | 100.00% | 45.56% | 74.36% | 82.02% | 9.69% |
| [borsh 1.5.7][borsh] | 23.08% | 31.57% | † | 33.43% | 63.80% | 71.15% | 3.46% |
| capnp:<br> [capnp 0.23.2][capnp] | 29.87% <span title="packed">*12.54%\**</span> | <span title="packed">*100.00%\**</span> | † | 18.57% <span title="packed">*30.53%\**</span> | 44.53% <span title="packed">*50.98%\**</span> | 53.18% <span title="packed">*54.99%\**</span> | 2.01% <span title="packed">*2.79%\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 17.15% | 11.98% | 4.91% | 13.45% | 43.35% | 54.42% | 2.07% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.47% | 5.80% | † | 13.45% | 43.35% | 54.42% | 2.08% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 6.79% | 12.31% | 5.03% | 13.45% | 43.35% | 54.42% | 2.05% |
| [columnar 0.11.1][columnar] | 43.77% | 30.43% <span title="copy_from">*75.67%\**</span> | † | 26.48% | 59.85% | 68.62% | 4.44% |
| [compactly 0.1.6][compactly] | 1.10% | 5.08% | † | 100.00% | 100.00% | 100.00% | 100.00% |
| [databuf 0.5.0][databuf] | 43.45% | 33.00% | 22.05% | 41.90% | 70.14% | 75.25% | 3.50% |
| [dlhn 0.1.7][dlhn] | 18.46% | 21.13% | † | 40.73% | 67.74% | 72.62% | 3.53% |
| [flatbuffers 25.12.19][flatbuffers] | 3.91% | † | † | 17.57% | 42.96% | 50.63% | 2.05% |
| [flexbuffers 25.2.10][flexbuffers] | 1.65% | 8.40% | 3.08% | 12.57% | 26.80% | 26.96% | 1.14% |
| json:<br> [flexon 0.4.5][flexon] | 4.81% | 12.61% | † | 9.20% | 32.03% | 41.57% | 1.25% |
| json:<br> [serde_json 1.0.140][serde_json] | 3.49% | 8.24% | † | 9.20% | 32.03% | 41.57% | 1.25% |
| json:<br> [simd-json 0.15.1][simd-json] | 5.76% | 12.60% | † | 9.20% | 32.03% | 41.57% | 1.21% |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 39.18% | 20.25% | 12.88% | 38.16% | 63.08% | 67.74% | 3.02% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 8.49% | 19.11% | 9.95% | 35.17% | 60.94% | 66.04% | 3.12% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 33.31% | 25.71% | 18.61% | 35.89% | 61.29% | 66.37% | 3.13% |
| [minicbor 1.0.0][minicbor] | 21.93% | 16.91% | 9.19% | 34.82% | 59.81% | 65.30% | 3.18% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.53% | 15.13% | 6.42% | 33.19% | 59.20% | 64.64% | 3.04% |
| [nanoserde 0.2.1][nanoserde] | 48.29% | 30.03% | † | 26.28% | 62.28% | 64.39% | 2.92% |
| [nibblecode 0.1.0][nibblecode] | 72.54% | † | † | 24.72% | 34.61% | 36.52% | 1.99% |
| [postcard 1.1.1][postcard] | 28.52% | 27.59% | 21.44% | 40.62% | 67.34% | 72.04% | 3.49% |
| [pot 3.0.1][pot] | 5.38% | 9.42% | 3.51% | 24.92% | 49.95% | 60.28% | 2.58% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*10.13%\**</span> <span title="populate + encode">*4.24%\**</span> | 15.98% | † | 25.01% | 48.94% | 55.56% | 2.40% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*12.17%\**</span> <span title="populate + encode">*4.25%\**</span> | 14.98% | † | 25.01% | 48.94% | 55.56% | 2.36% |
| [rkyv 0.8.10][rkyv] | 39.10% | <span title="unvalidated">*37.71%\**</span> <span title="validated upfront with error">*30.68%\**</span> | † | 24.73% | 58.65% | 68.04% | 3.05% |
| [ron 0.10.1][ron] | 1.69% | 2.24% | 0.73% | 10.19% | 34.36% | 43.54% | 1.27% |
| [savefile 0.18.6][savefile] | 59.64% | 30.06% | † | 26.33% | 62.43% | 64.50% | 2.91% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 20.85% | 27.48% | † | 41.90% | 70.16% | 75.25% | 3.68% |
| [serde-brief 0.1.1][serde-brief] | 10.47% | 11.08% | 4.88% | 11.70% | 39.97% | 50.89% | 1.95% |
| [serde_bare 0.5.0][serde_bare] | 16.75% | 24.15% | † | 41.90% | 70.14% | 75.25% | 3.61% |
| [speedy 0.8.7][speedy] | 47.64% | 33.65% | 30.41% | 33.21% | 63.60% | 71.03% | 3.32% |
| [wincode 0.5.3][wincode] | 61.90% | 34.86% | 30.59% | 26.33% | 62.43% | 64.50% | 2.86% |
| [wiring 0.2.4][wiring] | 62.24% | 29.75% | † | 26.33% | 60.30% | 66.33% | 2.82% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.81%\**</span> | <span title="validated on-demand with error">*38.12%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 0.14% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.97%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*11.00%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.06%\**</span> | <span title="unvalidated">*98.21%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.94%\**</span> <span title="validated upfront with error">*0.05%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `mk48`

This data set is composed of mk48.io game updates that contain data with many exploitable patterns and invariants.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*4.5002 ms\**</span> <span title="prepend">*2.5414 ms\**</span> | 8.5426 ms | 1704643 | 1294259 | 1245668 | 11.950 ms |
| [bin-proto 0.12.7][bin-proto] | 5.4233 ms | 5.3007 ms | 1791489 | 1127998 | 1051146 | 10.553 ms |
| [bincode 2.0.1][bincode] | 1.4807 ms | 3.8132 ms | 1406257 | 1117802 | 1062438 | 9.5133 ms |
| [bincode 1.3.3][bincode1] | 3.8834 ms | 4.3171 ms | 1854234 | 1141994 | 1048745 | 11.159 ms |
| [bitcode 0.6.6][bitcode] | 706.50 µs | 2.3706 ms | 971318 | 878034 | 850340 | 2.9382 ms |
| [borsh 1.5.7][borsh] | 2.9284 ms | 2.8970 ms | 1521989 | 1108471 | 1038528 | 10.552 ms |
| capnp:<br> [capnp 0.23.2][capnp] | 2.1204 ms <span title="packed">*4.1015 ms\**</span> | <span title="packed">*1.9156 ms\**</span> | 2724288 <span title="packed">*1616255\**</span> | 1546992 <span title="packed">*1278764\**</span> | 1239111 <span title="packed">*1125654\**</span> | 14.860 ms <span title="packed">*8.6516 ms\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 3.2443 ms | 18.457 ms | 6012539 | 1695215 | 1464951 | 21.433 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 23.673 ms | 53.216 ms | 6012373 | 1695146 | 1465025 | 21.376 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 10.248 ms | 20.125 ms | 6012373 | 1695146 | 1465025 | 21.055 ms |
| [columnar 0.11.1][columnar] | 908.22 µs | 3.7608 ms <span title="copy_from">*1.2702 ms\**</span> | 1544752 | 996728 | 897073 | 4.6615 ms |
| [compactly 0.1.6][compactly] | 64.111 ms | 56.194 ms | 802662 | 803238 | 802689 | 289.17 µs |
| [databuf 0.5.0][databuf] | 1.3198 ms | 3.7274 ms | 1319999 | 1062631 | 1008334 | 8.8912 ms |
| [dlhn 0.1.7][dlhn] | 4.4475 ms | 7.3507 ms | 1311281 | 1077520 | 1046095 | 8.6038 ms |
| [flatbuffers 25.12.19][flatbuffers] | 4.9613 ms | † | 2325620 | 1439185 | 1268060 | 13.580 ms |
| [flexbuffers 25.2.10][flexbuffers] | 39.910 ms | 35.686 ms | 5352680 | 2658295 | 2777967 | 34.695 ms |
| json:<br> [flexon 0.4.5][flexon] | 15.416 ms | 24.224 ms | 9390461 | 2391679 | 1842767 | 34.500 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 21.129 ms | 31.308 ms | 9390461 | 2391679 | 1842767 | 34.790 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 12.104 ms | 25.627 ms | 9390461 | 2391679 | 1842767 | 34.987 ms |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 945.70 µs | 5.5909 ms | 1458773 | 1156055 | 1137788 | 9.6440 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 10.555 ms | 10.986 ms | 1745322 | 1261627 | 1228923 | 11.539 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 1.8303 ms | 5.9209 ms | 1794467 | 1273669 | 1242301 | 11.730 ms |
| [minicbor 1.0.0][minicbor] | 2.3533 ms | 11.651 ms | 1777386 | 1276218 | 1252558 | 12.690 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 29.955 ms | 16.148 ms | 1770060 | 1277755 | 1263362 | 12.603 ms |
| [nanoserde 0.2.1][nanoserde] | 1.3047 ms | 2.7739 ms | 1812404 | 1134820 | 1053109 | 10.608 ms |
| [nibblecode 0.1.0][nibblecode] | 504.91 µs | † | 2075936 | 1541387 | 1433268 | 13.987 ms |
| [postcard 1.1.1][postcard] | 1.7848 ms | 4.2846 ms | 1311281 | 1083900 | 1041434 | 8.6521 ms |
| [pot 3.0.1][pot] | 14.119 ms | 29.854 ms | 2604812 | 1482233 | 1298928 | 16.054 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*5.4253 ms\**</span> <span title="populate + encode">*9.3319 ms\**</span> | 9.1814 ms | 1859886 | 1338076 | 1295351 | 12.327 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*5.5704 ms\**</span> <span title="populate + encode">*12.744 ms\**</span> | 12.061 ms | 1859886 | 1338076 | 1295351 | 12.176 ms |
| [rkyv 0.8.10][rkyv] | 961.42 µs | <span title="unvalidated">*2.2010 ms\**</span> <span title="validated upfront with error">*2.6206 ms\**</span> | 2075936 | 1383779 | 1210377 | 13.287 ms |
| [ron 0.10.1][ron] | 42.279 ms | 161.53 ms | 8677703 | 2233642 | 1826180 | 34.456 ms |
| [savefile 0.18.6][savefile] | 868.00 µs | 2.8395 ms | 1791505 | 1128012 | 1051153 | 10.168 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 3.1370 ms | 3.3375 ms | 1319999 | 1064380 | 1010708 | 8.8768 ms |
| [serde-brief 0.1.1][serde-brief] | 5.4464 ms | 21.925 ms | 6951772 | 1796265 | 1567819 | 26.188 ms |
| [serde_bare 0.5.0][serde_bare] | 4.8562 ms | 5.0070 ms | 1319999 | 1062645 | 1008349 | 8.8723 ms |
| [speedy 0.8.7][speedy] | 773.27 µs | 2.4632 ms | 1584734 | 1119837 | 1037992 | 10.326 ms |
| [wincode 0.5.3][wincode] | 563.73 µs | 2.3035 ms | 1791489 | 1127998 | 1051146 | 10.482 ms |
| [wiring 0.2.4][wiring] | 644.05 µs | 2.7683 ms | 1791489 | 1156963 | 1082815 | 10.517 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*68.757 ns\**</span> | <span title="validated on-demand with error">*1.0187 µs\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 57.959 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4915 ns\**</span> <span title="validated upfront with error">*5.3245 ms\**</span> | <span title="unvalidated">*2.7672 µs\**</span> <span title="validated upfront with error">*5.3297 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2456 ns\**</span> <span title="validated upfront with error">*343.95 µs\**</span> | <span title="unvalidated">*378.58 ns\**</span> <span title="validated upfront with error">*342.94 µs\**</span> | <span title="unvalidated">*238.56 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2450 ns\**</span> <span title="validated upfront with error">*428.51 µs\**</span> | <span title="unvalidated">*385.39 ns\**</span> <span title="validated upfront with error">*428.03 µs\**</span> | <span title="unvalidated">*236.86 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*11.22%\**</span> <span title="prepend">*19.87%\**</span> | 14.87% | 47.09% | 62.06% | 64.44% | 2.42% |
| [bin-proto 0.12.7][bin-proto] | 9.31% | 23.96% | 44.80% | 71.21% | 76.36% | 2.74% |
| [bincode 2.0.1][bincode] | 34.10% | 33.31% | 57.08% | 71.86% | 75.55% | 3.04% |
| [bincode 1.3.3][bincode1] | 13.00% | 29.42% | 43.29% | 70.34% | 76.54% | 2.59% |
| [bitcode 0.6.6][bitcode] | 71.47% | 53.58% | 82.64% | 91.48% | 94.40% | 9.84% |
| [borsh 1.5.7][borsh] | 17.24% | 43.85% | 52.74% | 72.46% | 77.29% | 2.74% |
| capnp:<br> [capnp 0.23.2][capnp] | 23.81% <span title="packed">*12.31%\**</span> | <span title="packed">*66.31%\**</span> | 29.46% <span title="packed">*49.66%\**</span> | 51.92% <span title="packed">*62.81%\**</span> | 64.78% <span title="packed">*71.31%\**</span> | 1.95% <span title="packed">*3.34%\**</span> |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 15.56% | 6.88% | 13.35% | 47.38% | 54.79% | 1.35% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 2.13% | 2.39% | 13.35% | 47.38% | 54.79% | 1.35% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 4.93% | 6.31% | 13.35% | 47.38% | 54.79% | 1.37% |
| [columnar 0.11.1][columnar] | 55.59% | 33.77% <span title="copy_from">*100.00%\**</span> | 51.96% | 80.59% | 89.48% | 6.20% |
| [compactly 0.1.6][compactly] | 0.79% | 2.26% | 100.00% | 100.00% | 100.00% | 100.00% |
| [databuf 0.5.0][databuf] | 38.26% | 34.08% | 60.81% | 75.59% | 79.61% | 3.25% |
| [dlhn 0.1.7][dlhn] | 11.35% | 17.28% | 61.21% | 74.55% | 76.73% | 3.36% |
| [flatbuffers 25.12.19][flatbuffers] | 10.18% | † | 34.51% | 55.81% | 63.30% | 2.13% |
| [flexbuffers 25.2.10][flexbuffers] | 1.27% | 3.56% | 15.00% | 30.22% | 28.89% | 0.83% |
| json:<br> [flexon 0.4.5][flexon] | 3.28% | 5.24% | 8.55% | 33.58% | 43.56% | 0.84% |
| json:<br> [serde_json 1.0.140][serde_json] | 2.39% | 4.06% | 8.55% | 33.58% | 43.56% | 0.83% |
| json:<br> [simd-json 0.15.1][simd-json] | 4.17% | 4.96% | 8.55% | 33.58% | 43.56% | 0.83% |
| messagepack:<br> [msgpacker 0.7.1][msgpacker] | 53.39% | 22.72% | 55.02% | 69.48% | 70.55% | 3.00% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 4.78% | 11.56% | 45.99% | 63.67% | 65.32% | 2.51% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 27.59% | 21.45% | 44.73% | 63.06% | 64.61% | 2.47% |
| [minicbor 1.0.0][minicbor] | 21.46% | 10.90% | 45.16% | 62.94% | 64.08% | 2.28% |
| [nachricht-serde 0.4.0][nachricht-serde] | 1.69% | 7.87% | 45.35% | 62.86% | 63.54% | 2.29% |
| [nanoserde 0.2.1][nanoserde] | 38.70% | 45.79% | 44.29% | 70.78% | 76.22% | 2.73% |
| [nibblecode 0.1.0][nibblecode] | 100.00% | † | 38.67% | 52.11% | 56.00% | 2.07% |
| [postcard 1.1.1][postcard] | 28.29% | 29.65% | 61.21% | 74.11% | 77.08% | 3.34% |
| [pot 3.0.1][pot] | 3.58% | 4.25% | 30.81% | 54.19% | 61.80% | 1.80% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*9.31%\**</span> <span title="populate + encode">*5.41%\**</span> | 13.83% | 43.16% | 60.03% | 61.97% | 2.35% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*9.06%\**</span> <span title="populate + encode">*3.96%\**</span> | 10.53% | 43.16% | 60.03% | 61.97% | 2.37% |
| [rkyv 0.8.10][rkyv] | 52.52% | <span title="unvalidated">*57.71%\**</span> <span title="validated upfront with error">*48.47%\**</span> | 38.67% | 58.05% | 66.32% | 2.18% |
| [ron 0.10.1][ron] | 1.19% | 0.79% | 9.25% | 35.96% | 43.95% | 0.84% |
| [savefile 0.18.6][savefile] | 58.17% | 44.73% | 44.80% | 71.21% | 76.36% | 2.84% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 16.10% | 38.06% | 60.81% | 75.47% | 79.42% | 3.26% |
| [serde-brief 0.1.1][serde-brief] | 9.27% | 5.79% | 11.55% | 44.72% | 51.20% | 1.10% |
| [serde_bare 0.5.0][serde_bare] | 10.40% | 25.37% | 60.81% | 75.59% | 79.60% | 3.26% |
| [speedy 0.8.7][speedy] | 65.30% | 51.57% | 50.65% | 71.73% | 77.33% | 2.80% |
| [wincode 0.5.3][wincode] | 89.57% | 55.14% | 44.80% | 71.21% | 76.36% | 2.76% |
| [wiring 0.2.4][wiring] | 78.40% | 45.88% | 44.80% | 69.43% | 74.13% | 2.75% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| capnp:<br> [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.81%\**</span> | <span title="validated on-demand with error">*37.16%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 2.15% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.97%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*13.68%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.95%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.11%\**</span> | <span title="unvalidated">*99.29%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*98.23%\**</span> <span title="validated upfront with error">*0.09%\**</span> | <span title="unvalidated">*100.00%\**</span> |

[bilrost]: https://crates.io/crates/bilrost/0.1013.0
[bin-proto]: https://crates.io/crates/bin-proto/0.12.7
[bincode]: https://crates.io/crates/bincode/2.0.1
[bincode1]: https://crates.io/crates/bincode/1.3.3
[bitcode]: https://crates.io/crates/bitcode/0.6.6
[borsh]: https://crates.io/crates/borsh/1.5.7
[capnp]: https://crates.io/crates/capnp/0.23.2
[cbor4ii]: https://crates.io/crates/cbor4ii/1.0.0
[ciborium]: https://crates.io/crates/ciborium/0.2.2
[columnar]: https://crates.io/crates/columnar/0.11.1
[compactly]: https://crates.io/crates/compactly/0.1.6
[databuf]: https://crates.io/crates/databuf/0.5.0
[dlhn]: https://crates.io/crates/dlhn/0.1.7
[flatbuffers]: https://crates.io/crates/flatbuffers/25.12.19
[flexbuffers]: https://crates.io/crates/flexbuffers/25.2.10
[flexon]: https://crates.io/crates/flexon/0.4.5
[minicbor]: https://crates.io/crates/minicbor/1.0.0
[msgpacker]: https://crates.io/crates/msgpacker/0.7.1
[nachricht-serde]: https://crates.io/crates/nachricht-serde/0.4.0
[nanoserde]: https://crates.io/crates/nanoserde/0.2.1
[nibblecode]: https://crates.io/crates/nibblecode/0.1.0
[parity-scale-codec]: https://crates.io/crates/parity-scale-codec/3.7.5
[postcard]: https://crates.io/crates/postcard/1.1.1
[pot]: https://crates.io/crates/pot/3.0.1
[prost]: https://crates.io/crates/prost/0.14.1
[protobuf]: https://crates.io/crates/protobuf/3.7.2
[rkyv]: https://crates.io/crates/rkyv/0.8.10
[rmp-serde]: https://crates.io/crates/rmp-serde/1.3.0
[ron]: https://crates.io/crates/ron/0.10.1
[savefile]: https://crates.io/crates/savefile/0.18.6
[serde-brief]: https://crates.io/crates/serde-brief/0.1.1
[serde_bare]: https://crates.io/crates/serde_bare/0.5.0
[serde_cbor]: https://crates.io/crates/serde_cbor/0.11.2
[serde_json]: https://crates.io/crates/serde_json/1.0.140
[simd-json]: https://crates.io/crates/simd-json/0.15.1
[speedy]: https://crates.io/crates/speedy/0.8.7
[wincode]: https://crates.io/crates/wincode/0.5.3
[wiring]: https://crates.io/crates/wiring/0.2.4
[zerompk]: https://crates.io/crates/zerompk/0.3.2


## Footnotes:

\* *mouse over for situational details*

† *this deserialization capability is not supported*

‡ *buffer mutation is not supported (`capnp` and `flatbuffers` may but not for rust)*
