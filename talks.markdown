---
layout: page
title: Talks
permalink: /talks/
---

<!--
I would like to have it with the talks like we have it with the posts.
That I have a folder _talks and a layout talk, and then just add
a few variables in the YAML front matter and then an automatically
generated list of the talks in this page.

But for now we do everything within this file with custom
styles and html-code.

-->


<!--Polymorphism Decision Table-->
<div>

<h1>Polymorphism Decision Table</h1>

<section>

  <nav>
    <ul>
      <li><a href="https://youtu.be/vzi0lTVyb-g?t=1730">Video</a></li>
      <li><a href="/assets/slides/C++%20London%20-%20May%202019%20-%20PolymorphismDecisionTable.pdf">Slides</a></li>
      <li><a href="https://www.meetup.com/de-DE/CppLondon/events/268533324/">C++ London</a></li>
      <li>May, 2020</li>
    </ul>
  </nav>

  <article>
    Based on four categories the Polymorphism Decision Table shows us when we can use which kind of polymorphism in C++.
  </article>

</section>

</div>


<br/>


<!--Execute Around Pointer-->
<div>

<h1>Execute Around Pointer</h1>

<section>

  <nav>
    <ul>
	  <li><a href="https://www.youtube.com/watch?v=4HnwuR_bFqs">Video</a></li>
      <li><a href="/assets/slides/Core%20C++%20-%20May%202019%20-%20ExecuteAroundPointer.pdf">Slides</a></li>
      <li><a href="https://www.meetup.com/de-DE/CoreCpp/events/270703090/">Core C++</a></li>
      <li>May, 2020</li>
    </ul>
  </nav>

  <article>
    The Execute Around Pointer is a simple, general and efficient solution to the problem of wrapping calls to an object in pairs of prefix and suffix code.
  </article>

</section>

</div>


<br/>


<!--C++ is a resource-safe language-->
<div>

<h1>C++ is a resource-safe language</h1>

<section>

  <nav>
    <ul>
	  <li><a href="https://www.youtube.com/watch?v=UmdU-y50tW0">Video</a></li>
      <li><a href="/assets/slides/embo++%20-%20C++%20is%20a%20resource-safe%20language.pdf">Slides</a></li>
      <li><a href="https://www.embo.io//">emBO++ 2021</a></li>
      <li>March, 2021</li>
    </ul>
  </nav>

  <article>
    When I started learning C++, I have been told many times that it is a difficult to learn programming language.
For several reasons. One reason was, that it does not have a garbage collector or other kind of built-in resource management.
During my increasing experience with C++ I was pleased to recognize that quite the opposite is the case.
C++ has all the tools at hand to write resource safe code.
  </article>

</section>

</div>


<br/>


<!--Deduction Guides for Range Adaptors-->
<div>

<h1>Deduction Guides for Range Adaptors</h1>

<section>

  <nav>
    <ul>
	  <li><a href="https://www.youtube.com/watch?v=k0GdNrrO6HE">Video</a></li>
      <li><a href="/assets/slides/embo++2022%20-%20Deduction%20Guides%20for%20Range%20Adaptors.pdf">Slides</a></li>
	  <li><a href="https://www.embo.io">emBO++ 2022</a></li>
      <li>March, 2022</li>
    </ul>
  </nav>

  <article>
	The Ranges library is part of the STL since C++20.
A lot of teaching material is available online already.
Even though most of this teaching material uses range adaptors (e.g. std::views::transform)
to adapt both lvalue and rvalue ranges, the underlying mechanism is mentioned briefly at most.
This talk will close this knowledge gap. 
It will explain the differences between adapting an lvalue and an rvalue,
and how the range adaptors deduction guides, while not at all visible to a user, make the key difference.
  </article>

</section>

</div>


<br/>


<!--Brace Yourselves, std::to_underlying is coming-->
<div>

<h1>Brace Yourselves, std::to_underlying is coming</h1>

<section>

  <nav>
    <ul>
      <li><a href="/assets/slides/MUC++-April%202022%20-%20BraceYourselves_std_to_underlying_is_coming.pdf">Slides</a></li>
      <li><a href="https://www.meetup.com/de-DE/MUCplusplus/events/284825082/">MUC++</a></li>
      <li>April, 2022</li>
    </ul>
  </nav>

  <article>
	C++23 will standardize the utility function std::to_underlying. This talk will present how this addition to the STL can break your
existing code base, as well as present solutions for how to solve this. 
  </article>

</section>

</div>


<br/>


<!--75 STL Headers in under 10 minutes-->
<div>

<h1>75 STL Headers in under 10 minutes</h1>

<section>

  <nav>
    <ul>
      <li><a href="/assets/slides/Meeting%20C++-UG-August2022-75%20STL%20Headers%20in%20under%2010%20minutes.pdf">Slides</a></li>
      <li><a href="https://www.meetup.com/meeting-cpp-online/events/287010750/">Meeting C++ online</a></li>
      <li>August, 2022</li>
    </ul>
  </nav>

  <article>
	In C++20, the STL consists of 75 headers (excluding deprecated headers and those from the C standard library).
	During this lightning talk we will rush trough all of them and get a brief overview of what they contain.
  </article>

</section>

</div>
