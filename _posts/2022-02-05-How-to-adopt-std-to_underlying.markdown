---
layout: post
title: "How to adbot sdt::to_underlying"
date: 2022-02-05
author: Kilian Henneberger
---

# How to adopt ``std::to_underlying``
As you probably know, it is not possible to print an enum in C++ out of the box.



This is so common, that this small utility function got to C++23, under the name ``std::to_underlying``.
While this is a small, yet great addition to the STL, it will take some effort to adopt your code base to it.
GCC 11.x is currently 


First snippet
```C++
#include <array> //std::array
#include <charconv> //std::to_chars
#include <iostream> //std::cout
#include <type_traits> //std::underlying_type_t

template<class Enum>
constexpr auto to_underlying(Enum e) noexcept
{
    using UT = std::underlying_type_t<Enum>;
    return static_cast<UT>(e);
}

int main()
{
    std::array<char, 3> textBuffer;
    char* first = textBuffer.data();
    char* last = first + textBuffer.size();
    auto [ptr, ec] = std::to_chars(first, last, 1234);
    if (ec == std::errc()) {
        std::cout << "Success";
    }
    else {
        std::cout << "to_chars returned an error: " << to_underlying(ec);
    }
}
```
Godbolt: https://godbolt.org/z/rsnaKjs6q


Second snippet with C++2b

```
Gleiches wie erstes snippet, aber mit -std=c++2b
```
Godbolt: https://godbolt.org/z/6axWPzxzG



## Further Sources


### [``std::to_underlying``](https://en.cppreference.com/w/cpp/utility/to_underlying)

### [P1682R3 std::to_underlying for enumerations](https://wg21.link/P1682R3)

### [Feature test macros](https://en.cppreference.com/w/cpp/utility/feature_test)

### [Argument-dependent lookup](https://en.cppreference.com/w/cpp/language/adl)