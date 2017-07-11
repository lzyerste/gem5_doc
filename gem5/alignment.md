两种对齐方式：向低（下）对齐与向高（上）对齐，姑且称之为align_floor()与align_ceil()。

dram_ctrl（mem/dram_ctrl.hh）中需要对请求的地址进行对齐，向低对齐的方式：

```cpp
Addr burstAlign(Addr addr) const { return (addr & ~(Addr(burstSize - 1))); }
```

即先生成低位全为1的，然后取反，再与操作。

一个dram request可能分成多个dram packet，即分成多次burst，下一个基址需要对齐（在函数DRAMCtrl::addToReadQueue中）：

```cpp
addr = (addr | (burstSize - 1)) + 1;
```

即先将地址的低位全或成1，然后地址加1即可（对齐）。

------

另外的实现，参考base/intmath.hh，roundUp()为向上对齐，roundDown()为向下对齐。

```cpp
template <class T, class U>
inline T
roundUp(const T& val, const U& align)
{
    T mask = (T)align - 1;
    return (val + mask) & ~mask;
}

template <class T, class U>
inline T
roundDown(const T& val, const U& align)
{
    T mask = (T)align - 1;
    return val & ~mask;
}
```

