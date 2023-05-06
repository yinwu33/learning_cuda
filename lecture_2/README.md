# 矩阵乘法

```CUDA
// 静态申请
__global__ void staticReverse(int *d, int n) {
    __shared__ int s[64];
    int t = threadIdx.x;
    int tr = n - t - 1;
    s[t] = d[t];
    __syncthreads();
    d[t] = s[tr];
}

staticReverse<<<1, n>>>(d_d, n);

// 动态申请
__global__ void dynamicReverse(int *d, int n) {
    extern __shared__ int s[];  // 注意extern关键字
    int t = threadIdx.x;
    int tr = n - t - 1;
    s[t] = d[t];
    __syncthreads();
    d[t] = s[tr];
}

dynamicReverse<<<1, n, n * sizeof(int)>>>(d_d, n);  // 调用的时候需要传入第三个参数，来明确核函数需要申请多少共享内存
```