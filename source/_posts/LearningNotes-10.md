---
title: C++STL中vector的基本原理和方法实现
tags: 
    - C++
    - 编程 
categories: 学习笔记
date: 2022-11-11 00:05:03
---
## 概述
vector容器具有以下基本特点-连续存储，长度灵活，随机访问。在stl_vector.h中可以看到<code>vector</code>继承自一个结构体基类<code>_Vector_base</code>，其中<code>_Vector_impl_data</code>结构体定义了三个存储<code>vector</code>关键位置的指针，即开始位置，结束位置和最大长度位置。
~~~
    struct _Vector_impl_data
        {
        pointer _M_start;
        pointer _M_finish;
        pointer _M_end_of_storage;
        }
~~~
对于<code>_M_start</code>与<code> _M_finish</code>很好理解，它指向了连续内存的开始和结束位置。但对于<code>_M_end_of_storage</code>需要注意的是它表示的是当前vecor容器的可用空间的尾部，意味着对与容器的扩容操作，他需要执行以下步骤
- 先检查当前是否还存在可用空间，即<code>_M_finish</code>是否等于<code>_M_end_of_storage</code>，如果成立，则跳到2，不成立跳到3
- 构造一个新的元素并插入<code>vector</code>中，并调整<code>_M_finish</code>指针
- 调用_M_realloc_insert，另寻他处，重新开辟空间，将原来的<code>vector</code>中的元素都拷贝到新的<code>vector</code>中，并将新元素也插入<code>vector</code>中，并销毁原来的<code>vector</code>以及其中的元素

        emplace_back(_Args&&... __args)
        {
        if (this->_M_impl._M_finish != this->_M_impl._M_end_of_storage)
        {
            _GLIBCXX_ASAN_ANNOTATE_GROW(1);
            _Alloc_traits::construct(this->_M_impl, this->_M_impl._M_finish,
                        std::forward<_Args>(__args)...);
            ++this->_M_impl._M_finish;
            _GLIBCXX_ASAN_ANNOTATE_GREW(1);
        }
        else
        _M_realloc_insert(end(), std::forward<_Args>(__args)...);
意味着超出内存空间的插入操作是不友好的。

### 插入操作
<code>vector</code>允许在连续空间的末尾执行插入和删除操作。 若要在<code>vector</code>中间插入或删除元素，则需要线性时间。插入操作具体代码较多，大致描述下插入操作的步骤。<span class="heimu">代码没看懂，之后再看看《STL源码刨析》理解下</span>

- 检查插入的元素个数n是否为0
- 检查可用空间是否大于等于n，如果此条成立还需要区分新插入的元素个素n与安插点之后的元素个数的大小情况
    - 成立
        - 插入位置之后整体后移
        - 调整尾指针<code> _M_finish</code>
        - 拷贝插入点的值到对应位置
        - 在插入点填充值
    - 不成立
        - 配置新空间
        - 拷贝插入位置之前的部分
        - 插入待插入元素
        - 拷贝剩余部分

## 方法列表
|名称|	说明|
|---|---|
|assign|	清除矢量并将指定的元素复制到该空矢量。|
|at|	返回对矢量中指定位置的元素的引用。|
|back	|返回对向量中最后一个元素的引用。|
|begin	|对该向量中第一个元素返回随机访问迭代器。|
|capacity|	返回在不分配更多的存储的情况下向量可以包含的元素数。|
|cbegin	|返回指向向量中第一个元素的随机访问常量迭代器。|
|cend	|返回一个随机访问常量迭代器，它指向刚超过矢量末尾的位置。|
|crbegin	|返回一个指向反向矢量中第一个元素的常量迭代器。|
|crend|	返回一个指向反向矢量末尾的常量迭代器。|
|clear|	清除向量的元素。|
|data|	返回指向向量中第一个元素的指针。|
|emplace|	将就地构造的元素插入到指定位置的向量中。|
|emplace_back|	将一个就地构造的元素添加到向量末尾。|
|empty|	测试矢量容器是否为空。|
|end|	返回指向矢量末尾的随机访问迭代器。|
|erase	|从指定位置删除向量中的一个元素或一系列元素。|
|front	|返回对向量中第一个元素的引用。|
|get_allocator|	将对象返回到矢量使用的 allocator 类。|
|insert|	将一个元素或多个元素插入到指定位置的向量中。|
|max_size|	返回向量的最大长度。|
|pop_back	|删除矢量末尾处的元素。|
|push_back	|在矢量末尾处添加一个元素。|
|rbegin	|返回指向反向向量中第一个元素的迭代器。|
|rend|	返回一个指向反向矢量末尾的迭代器。|
|reserve|	保留向量对象的最小存储长度。|
|resize|	为矢量指定新的大小。|
|shrink_to_fit|	放弃额外容量。|
|size|	返回向量中的元素数量。|
|swap|	交换两个向量的元素。|

## 总结
- <code>vector</code>内部为连续的内存空间，基于此它仍然和数组一样属于易查找难扩展的。
- 具体的，应该尽可能规避可能触发扩容操作的行为
