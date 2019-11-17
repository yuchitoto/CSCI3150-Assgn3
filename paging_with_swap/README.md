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

Use PFN stored in page table to locate resource in disk

```c
swap_page_id = kernel->si->swapper_space[pfn];
fseek(f, swap_page_id * PAGE_SIZE, SEEK_SET);
fwrite(kernel->space + PAGE_SIZE * pfn, sizeof(char), sizeof(char) * PAGE_SIZE, f);
memset(kernel->space + PAGE_SIZE * pfn, 0, PAGE_SIZE);
```
