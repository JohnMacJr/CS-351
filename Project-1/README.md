# CS-351 Project-1: Performance Evaluation of Hash Programs

## Overview
This project looks at how different ways of handling memory and accessing data can change the performance of a hash program. We built five versions of the program, each using a different memory management methods. By comparing these, we can see how small implementation choices affect runtime, CPU load, and memory use. We also test how compiler optimizations improve performance.
##
| Program   | Opt Level           | Real Time (s) | User Time (s) | Sys Time (s) | Memory Usage (KB) | Throughput (MB/s) | Speedup over hash-00 (-g) |
|-----------|---------------------|---------------|----------------|---------------|--------------------|--------------------|----------------------------|
| hash-00   | -g                  | 353.61        | 341.70         | 9.91          | 2904               | 2.90               | 1.00x                      |
| hash-01   | -g                  | 22.07         | 16.94          | 2.53          | 2912               | 46.40              | 16.02x                     |
| hash-02   | -g                  | 15.48         | 14.26          | 1.11          | 3488               | 66.15              | 22.84x                     |
| hash-03   | -g                  | 16.51         | 15.09          | 1.28          | 2888               | 62.02              | 21.42x                     |
| hash-04   | -g                  | 14.26         | 13.77          | 0.41          | 5,011,808          | 71.83              | 24.80x                     |
| hash-00   | -O2                 | 344.32        | 332.14         | 9.13          | 2900               | 2.97               | 1.03x                      |
| hash-01   | -O2                 | 7.75          | 6.60           | 1.10          | 2908               | 132.00             | 45.63x                     |
| hash-02   | -O2                 | 8.00          | 6.86           | 1.08          | 2908               | 128.00             | 44.20x                     |
| hash-03   | -O2                 | 7.95          | 6.83           | 1.05          | 3484               | 128.68             | 44.47x                     |
| hash-04   | -O2                 | 7.05          | 6.61           | 0.37          | 5,012,380          | 145.39             | 50.15x                     |
| hash-00   | -O3 -funroll-loops | 335.14        | 329.51         | 3.89          | 2884               | 3.05               | 1.06x                      |
| hash-01   | -O3 -funroll-loops | 8.16          | 6.85           | 1.23          | 3468               | 125.49             | 43.34x                     |
| hash-02   | -O3 -funroll-loops | 7.92          | 6.79           | 1.05          | 3476               | 129.29             | 44.64x                     |
| hash-03   | -O3 -funroll-loops | 7.93          | 6.82           | 1.04          | 2908               | 129.13             | 44.59x                     |
| hash-04   | -O3 -funroll-loops | 7.05          | 6.60           | 0.38          | 5,012,380          | 145.39             | 50.15x                     |

##
1. What operation do you think accounts for most of hash-00's runtime?
- Most of hash-00's runtime consists of making repeated function calls and inneficient handling of memory. The lack of optimization is evdent in the extremely long   real and user times.

2. hash-01 and hash-02 both dynamically allocate memory for each hash computation.  Is there much difference time-wise between their two allocation methods?
- Yes, there is about a 6.5 second difference on -g between 01 and 02 but it is less evident under 02 and 03 optimization.

3. hash-03 avoids the allocation by using a fixed-size array.  Is there an appreciable speed difference?
- Yes, in some cases 03 performs slightly better than 02.

4. Why is hash-04's memory usage so much larger than any of the other versions? 
- Hash-04 uses memory-mapped I/O which means the operating system maps the entire file directly into the process’s memory space.

5. What other compiler options did you try, and did they help at all?
- I tested -O3 -funroll-loops. Only hash-00 showed minor improvements in run times.
