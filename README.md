# cub-benchmark

## Build Google Benchmark
```bash
$ cd benchmark
# Make a build directory to place the build output.
$ cmake -E make_directory "build"
# Generate build system files with cmake, and download any dependencies.
$ cmake -E chdir "build" cmake -DBENCHMARK_DOWNLOAD_DEPENDENCIES=on -DCMAKE_BUILD_TYPE=Release ../
# or, starting with CMake 3.13, use a simpler form:
# cmake -DCMAKE_BUILD_TYPE=Release -S . -B "build"
# Build the library.
$ cmake --build "build" --config Release && cd ..
```

## Compile the example App
```bash
$ nvcc -c -O3 segmented16_radix_sort.cu -o segmented16_radix_sort.o -Ibenchmark/include
$ nvcc segmented16_radix_sort.o -o segmented16_radix_sort -Ibenchmark/include -Lbenchmark/build/src -lbenchmark -lpthread
```

## Run App
```bash
$ ./segmented16_radix_sort --size 1287936
```

## Result
Docker: nvidia/cuda:11.8.0-cudnn8-devel-ubuntu20.04

- [CUDA] Device name: NVIDIA A100-PCIE-40GB
- 2023-12-04T19:09:25+08:00
- Running ./segmented16_radix_sort_cased
- Run on (256 X 2250 MHz CPU s)
- CPU Caches:
  - L1 Data 32 KiB (x128)
  - L1 Instruction 32 KiB (x128)
  - L2 Unified 512 KiB (x128)
  - L3 Unified 16384 KiB (x32)
- Load Average: 0.22, 0.35, 0.34

| Benchmark | Time | CPU | Iterations | UserCounters...|
| --------- | ---- | --- | ---------- | ------------------------- |
| sort_pairs<float, int>(~16 segments), descending/manual_time | 5.96 ms | 5.96 ms | 103 | bytes_per_second=6.44022Gi/s items_per_second=864.391M/s |