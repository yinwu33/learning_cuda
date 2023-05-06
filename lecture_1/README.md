# 函数速查

### cudaMalloc

内存申请

```c++
cudaError_t cudaMalloc();;
```

### cudaFree

释放内存

```c++
cudaError_t cudaFree(void* );
```

### cudaMemcpy

```c++
cudaError_t cudaMemcpy(void* dst, const void* src, size_t count, cudaMemcpyKind kind);

```

支持四种cudaMemcpyKind类型

* cudaMemcpyHostToDevice
* cudaMemcpyDeviceToHost
* cudaMemcpyDeviceToDevice
* cudaMemcpyDefault

### 

`dim3` 是内建类型，表明CUDA kernel的维度。例如：

```c++
dim3 block(2, 2);  // 定义一个二维的kernel维度，大小为2x2

kernel_name<<<grid, block>>>(args);
```

`grid`是block中具体的哪一个

# Kernel Function 核函数

* 通过__global__修饰
* 通过`<<<a, b>>>`说明核函数中的线程数量
* 以Grid形式组织，每个线程由若干个block组成

### 三种标识符

|            | 工作地点 | 被调用地点 |
| ---------- | -------- | ---------- |
| __device__ | device   | device     |
| __global__ | device   | host       |
| __host__   | host     | host       |
