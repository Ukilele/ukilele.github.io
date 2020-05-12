---
title: "Polymorphism Decision Table"
date: 2020-05-11
---

# Polymorphism Decision Table
A lot of programming languages (e.g. Java and C#) let a programmer achieve polymorphism via a base class
with pure virtual functions and derived classes that override these functions. C++ also provides this kind of polymorphism.
But C++ comes with additional ways to achieve polymorphism (**[variant](#variant)**, **[type erasure](#type-erasure)** and **[polymorphic_value](#polymorphic-value)**).
In this blog post I will not explain how these features work. There already exists a lot of material about them.
I rather want to focus on when to use which kind of polymorphism.
For that purpose I created a decision-table that tells you based on which criterions you can use which kind of polymorphism.

---

<style>
#customers {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#customers td, #customers th {
  border: 1px solid #ddd;
  padding: 8px;
  text-align:center;
}

#customers tr:nth-child(even){background-color: #f2f2f2;}

#customers tr:hover {background-color: #ddd;}

#customers th {
  padding-top: 12px;
  padding-bottom: 12px;
  background-color: green;
  color: white;
}

#customers td:nth-child(5) {
  background-color: #2C9F30;
  color: white;
  
}

</style>

<table id="customers">
  <tr>
    <th>Set of Types</th>
    <th>Set of Functions</th>
    <th>Semantics</th>
    <th>Base-Class</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Closed</td>
    <td>Value</td>
    <td>No</td>
    <td>variant</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Closed</td>
    <td>Value</td>
    <td>Yes</td>
    <td>PV, variant</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Closed</td>
    <td>Reference</td>
    <td>No</td>
    <td>TER, variant&lt;SP&gt;</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Closed</td>
    <td>Reference</td>
    <td>Yes</td>
    <td>SP</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Open</td>
    <td>Value</td>
    <td>No</td>
    <td>variant</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Open</td>
    <td>Value</td>
    <td>Yes</td>
    <td>PV+HVP, variant</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Open</td>
    <td>Reference</td>
    <td>No</td>
    <td>variant&lt;SP&gt;</td>
  </tr>
  <tr>
    <td>Closed</td>
    <td>Open</td>
    <td>Reference</td>
    <td>Yes</td>
    <td>SP+HVP, variant&lt;SP&gt;</td>
  </tr>
  <tr>
    <td>Open</td>
    <td>Closed</td>
    <td>Value</td>
    <td>No</td>
    <td>TEV</td>
  </tr>
  <tr>
    <td>Open</td>
    <td>Closed</td>
    <td>Value</td>
    <td>Yes</td>
    <td>PV</td>
  </tr>
  <tr>
    <td>Open</td>
    <td>Closed</td>
    <td>Reference</td>
    <td>No</td>
    <td>TER</td>
  </tr>
  <tr>
    <td>Open</td>
    <td>Closed</td>
    <td>Reference</td>
    <td>Yes</td>
    <td>SP</td>
  </tr>
</table>


PV = polymorphic_value  
TER = type erasue with reference semantics  
TEV = type erasue with value semantics  
SP = smart pointer  
HVP = hand-written visitor pattern

---

This decision-table is by no means complete. There exist further criterions that this table does not take into account.
Yet it is a helpful guide when one feels overwhelmed by the flexibility of C++.


### Further Sources

#### General
- [[MUC++] Klaus Iglberger - Embrace No Paradigm Programming!](https://www.youtube.com/watch?v=fwXaRH5ffJM)

#### Variant
- [Modern C++ Features - std\::variant and std::visit](https://arne-mertz.de/2018/05/modern-c-features-stdvariant-and-stdvisit/)
- [Everything You Need to Know About std::variant from C++17]( https://www.bfilipek.com/2018/06/variant.html)

#### Type Erasure
- [Better Code: Runtime Polymorphism - Sean Parent](https://www.youtube.com/watch?v=QGcVXgEVMJg)
- [C++Now 2018: Louis Dionne "Runtime Polymorphism: Back to the Basics"](https://www.youtube.com/watch?v=OtU51Ytfe04)
- [CppCon 2019: Arthur O'Dwyer "Back to Basics: Type Erasure"](https://www.youtube.com/watch?v=tbUCHifyT24)

#### Polymorphic Value
- [https://github.com/jbcoe/polymorphic_value](https://github.com/jbcoe/polymorphic_value)

