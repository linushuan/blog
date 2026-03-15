---
title: "STL in C++" # 標題
date: 2026-03-11T22:19:26+08:00 # 發布時間
draft: true # 草稿
description: "A useful default template in c++" # ani 摘要
summary: "A useful  default template in c++" # sim 摘要
author: "Linuk" # 作者

#　can put many in
tags: ["stl", "cp"] # 標籤
categories: ["CP"] # 分類

math: true            # Latex 支援
toc: true             # 是否顯示目錄 (Anatole 支援)

# picture put in static/
# thumbnail: "icon.png" # Anatole
cover: "etyear.webp"     # Reimu
---

## STL library
```cpp
#include <array>
#include <vector>
#include <bitset>
#include <utility>
#include <tuple>
#include <deque>
#include <stack>
#include <queue>
#include <list>
#include <set>
#include <map>
#include <bits/stdc++.h>
#include <bit/extc++.h> // gnu, just for g++
```

## template
可以放模板的東西
example:
```cpp
vector<int> vec1;
vector<double> vec2;
```
為什麼 `vector` 可以放 `int` 又可以放 `double`?
因為實際上 `vector` 裡面放的是 template 可以接受有定義運算(*註1)的型別

how to use:
```cpp
template <typename T>
class vector {

private:
    T* data_p;
    size_t _size, _capacity;
    void alloc(size_t new_capacity) {
        T* new_data
    }
    
public:
    vector() : data(nullptr), _size(0), _capacity(0) {}
    ~vector() {
        delete[] data;
    }
    void push_back

};
```


*註1: 有定義運算指的是在使用如 `<=>` `+-*/` 等運算/比較時有定義如何運作
