---
layout: post
title: "Execute-Around Pointer with Deducing this"
date: 2022-09-24
author: Kilian Henneberger
---

# Execute-Around Pointer with Deducing `this`
One of the new language features for C++23 is Deducing `this`. One of the authors
of that proposal is [Barry Revzin](https://twitter.com/BarryRevzin).
Recently he published a blog post [Copy-on-write with Deducing `this`](https://brevzin.github.io/c++/2022/09/23/copy-on-write/).
The essence of the blog post is, that the explicit object parameter can be of
a different type than the class in which a function gets declared
([link](https://brevzin.github.io/c++/2022/09/23/copy-on-write/#an-explicit-object-parameter-of-differing-type)).
While thinking of scenarios in which this could be of use, I remembered
the Execute-Around Pointer idiom. If not familiar with it, look up my [slides](https://ukilele.github.io/assets/slides/Core%20C++%20-%20May%202019%20-%20ExecuteAroundPointer.pdf)
or my [talk](https://www.youtube.com/watch?v=4HnwuR_bFqs). Briefly, the idea is to wrap calls to an object in a pair of prefix and suffix code. In the talk I presented a general solution to this problem. Here is what it looked like:

```c++
template<class Pointer, class Suffix>
class CallProxy {
    Pointer ptr;
    Suffix suf;
public:
    CallProxy(Pointer ptr, Suffix suf)
        : ptr(ptr), suf(suf) {}
    Pointer operator->() { return ptr; }
    ~CallProxy() { suf(); }
    CallProxy(const CallProxy&) = delete;
    CallProxy& operator=(const CallProxy&) = delete;
};

template<class Pointer, class Prefix, class Suffix>
class ExecuteAroundPointer {
    Pointer ptr;
    Prefix pre;
    Suffix suf;
public:
    ExecuteAroundPointer(Pointer ptr, Prefix pre, Suffix suf)
        : ptr(ptr), pre(pre), suf(suf) {}
    CallProxy<Pointer&, Suffix&> operator->() {
        pre();
        return CallProxy<Pointer&, Suffix&>(ptr, suf);
    }
};
```
A contrived use-case from a multithreaded environment might look like this:

```c++
std::string s; //the object that we are going to wrap in an ExecuteAroundPointer
std::mutex m; //the mutex that we are using to lock the access to `s`
auto prefix = [&]{ m.lock(); };
auto suffix = [&]{ m.unlock(); };
ExecuteAroundPointer p(&s, prefix, suffix); //every access trough `p` to `s` will appear within a locked mutex
auto action = [&] {
    for (int i = 0; i != 1'000; ++i) {
        p->append("X"); //if you change this to `s.append("X");` you'll get race conditions
    }
};
//start four threads that simultaneously access `p`
std::array futures = { std::async(action), std::async(action), std::async(action), std::async(action) };
for (auto& f : futures) f.wait();
std::cout << s.size(); //gonna print 4000
```

With the usage of Deducing `this`, we can further simplify the implementation of the `ExecuteAroundPointer`:
```c++
template<class Pointer, class Prefix, class Suffix>
class ExecuteAroundPointer {
    Pointer ptr;
    Prefix pre;
    Suffix suf;

    using Guard = std::experimental::scope_exit<Suffix&>;
    using PointerAndGuard = std::pair<Pointer&, Guard>;

public:
    ExecuteAroundPointer(Pointer ptr, Prefix pre, Suffix suf)
        : ptr(ptr), pre(pre), suf(suf) {}

    operator PointerAndGuard() {
        pre();
        return {ptr, Guard{suf}};
    }

    Pointer& operator->(this PointerAndGuard p) { return p.first; }
};
```

The whole code can be found on [godbolt](https://godbolt.org/z/cPvMoKMWe) (due to the lack of compiler support it uses the Circle compiler).
While the Execute-Around Pointer idiom is a niche in C++, I am still happy to 
utilise Deducing `this` to simplify my implementation of it.
