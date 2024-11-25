# CIS345project4

Purpose
---------

The objective of this project is to implement and optimize the FAXPY function using CUDA programming to gain familiarity with parallel processing on GPUs. The FAXPY function computes the result as:
result[i] = 𝑎*x[i] + y[i]
where x, y, result, and a are all single-precision floating-point values.

The implementation involves:

Writing CUDA kernels to perform FAXPY using a single block of threads and multiple blocks of threads.
Comparing performance between CPU implementation, single-block GPU kernel, and multi-block GPU kernel.
Measuring execution time for computational performance while excluding data transfer times.

Contributions:
----------------
In this group project, the breakdown would be:

([Manikdeep Kaur LNU]: 55% and [John Mendicino]: 45%) contribution to all aspects of the project, including CUDA kernel implementation, debugging, and performance evaluation.

Design Details
--------------

Kernel Implementations:

faxpy_1blk_kernel: Computes FAXPY using a single block of threads. Each thread handles one element of the input arrays.
faxpy_mblk_kernel: Computes FAXPY using multiple blocks of threads. The implementation uses global thread indexing to handle larger arrays efficiently.
Execution Sequence: The program follows these steps:

Allocate memory on the host and device.
Transfer input arrays (x and y) and scalar (a) from host to device.
Launch the FAXPY kernels:
faxpy_1blk_kernel: Single-block computation.
faxpy_mblk_kernel: Multi-block computation.
Copy results back to the host.
Compare the GPU results against the CPU implementation.
Measure and print execution times for:
CPU computation.
GPU single-block kernel.
GPU multi-block kernel.
Output correctness of GPU results.
Timing: The timing code ensures synchronization using cudaDeviceSynchronize() before capturing kernel execution times to accurately measure performance.

Execution Commands
------------------
Compile the program using nvcc:
===========================

nvcc -o cudaa cudaa.cu

Run the program:
================

./cudaa

Performance Observations:
========================

Execution Times:

CPU implementation: 43.481 ms
Single-block GPU kernel (faxpy_1blk_kernel): 68.142 ms
(Significantly slower for large arrays due to limited parallelism.)
Multi-block GPU kernel (faxpy_mblk_kernel): 22.857 ms
(Faster due to better utilization of GPU resources.)

Performance Comparison:
=======================

The multi-block GPU kernel outperformed both the CPU and single-block GPU kernel for large arrays.
Single-block GPU kernel performed worse than the CPU due to thread limitations.

Reason for Differences:
--------------------------

CPU: Sequential processing of elements.
Single-block kernel: Limited number of threads, causing insufficient parallelism for larger arrays.
Multi-block kernel: Effective utilization of thousands of threads, allowing better scalability for large arrays.

Sample Output
==============

Overall: 49.167 ms        [4.546 GB/s]
xy array --> device 17.336 ms
GPU computation duration 22.857 ms
CPU computation duration 43.481 ms
device faxpy outputs are correct!


Working and Non-Working Modules
-------------------------------

Working Modules:
================
CPU implementation.
Single-block GPU kernel.
Multi-block GPU kernel.
Memory management and correctness checks.

Non-Working Modules:
====================
None. All modules function as intended.

Conclusion
----------
This project demonstrated the benefits of parallel processing using CUDA. The multi-block kernel provided the best performance, especially for larger datasets, while the single-block kernel highlighted the limitations of insufficient parallelism.

