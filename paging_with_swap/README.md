# Paging with swapping
## swap
LRU stores the occupied page, head has the longest untouched time, tail has the least untouched time.

file: 'swap' is the disk storage

```c
kernel->si->swap_map = (char *)malloc(sizeof(char) * MAX_PROCESS_NUM * VIRTUAL_SPACE_SIZE / PAGE_SIZE);
kernel->si->swapper_space = (int *)malloc(sizeof(int) * KERNEL_SPACE_SIZE / PAGE_SIZE);
memset(kernel->si->swap_map, 0, sizeof(char) * MAX_PROCESS_NUM * VIRTUAL_SPACE_SIZE / PAGE_SIZE);
for(int i = 0; i < KERNEL_SPACE_SIZE / PAGE_SIZE; i++) {
  kernel->si->swapper_space[i] = -1;
```
