---
draft: false
banner: "A language for writing correct software!"
---
{{<section class="banner">}}
<div class="column">
<h1>Whiley</h1>

<i><h3>High integrity software at Scale</h3></i>
<ul class="ticklist">
<li>An open source programming language</li>
<li>Built in support for verification</li>
<li>Easy to learn and getting started with</li>
</ul>
<button class="bigbutton">Download</button>
<button class="bigbutton">Get Started</button>
</div>
<div class="column">
<div id="editor" class="ace-whiley">/**
 * Compute the maximum value of two integers
 */
function max(int x, int y) -> (int r)
// Ensure return not smaller than parameters
ensures (r >= x) && (r >= y)
// Ensure a parameter returned
ensures (r == x) || (r == y): 
   if x >= y:
      return x
   else:
      return y
</div>
</div>
{{</section>}}

{{<section>}}
<div class="column">
<h3>Reliability</h3>
Whiley employs state-of-the-art techniques for ensuring your
<b>software is correct</b>.  You can specify functions using <a
href="https://en.wikipedia.org/wiki/Precondition">preconditions</a>
and <a
href="https://en.wikipedia.org/wiki/Postcondition">postconditions</a>,
and then <a
href="https://en.wikipedia.org/wiki/Formal_verification">statically
verify</a> your implementation meets its specification.

</div>
<div class="column">
<h3>Open Source</h3>
Whiley is an independently developed open source project and is free
to use.  Join our community on our <a
href="https://discord.com/channels/825109901352632331/825109901352632334">Discord
forum</a>, follow us on <a
href="https://twitter.com/WhileyLang">Twitter</a> and contribute to
the code on <a href="http://github.com/Whiley">GitHub</a>.</div>

<div class="column">
<h3>Flexibility</h3>
Whiley supports <a
href="https://en.wikipedia.org/wiki/Functional_programming">functional</a>
and <a
href="https://en.wikipedia.org/wiki/Imperative_programming">imperative
programming</a> without being opinionated.  Whiley can be used to
develop web applications, smart contracts, embedded systems and more.
</div>
{{</section>}}

{{<section class="alternate">}}

<div class="column">
<iframe src="https://www.youtube.com/embed/MLcNhc27Ghw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<div class="column">
<iframe src="https://www.youtube.com/embed/yYGEcyCHiZk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<div class="column">
<iframe src="https://www.youtube.com/embed/1KfZH_jjrG4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

{{</section>}}

{{<section>}}
<div class="column">
<h3>Features</h3>
<ul class="ticklist">

<li><b>Specification.</b> Unlike most other programming languages, Whiley provides first-class support for specifying functions using preconditions and postconditions. </li>

<li><b>Static Typing.</b> Whiley is a <a href="https://en.wikipedia.org/wiki/Type_system#Static_type_checking">statically typed</a> programming language which employs <a href="https://www.google.com/search?channel=fs&client=ubuntu&q=type+inference">type inference</a> and <a href="https://en.wikipedia.org/wiki/Flow-sensitive_typing">flow typing</a> for ease of use.</li>

<li><b>Static Verification.</b> Whiley supports static verification technology to give sophisticated support for finding software errors.</li>

<li><b>Automated Testing.</b> Whiley supports automated testing (in the style of QuickCheck) to quickly check for errors and other problems. </li>

<li><b>Package Management.</b> Whiley has a small but growing selection of packages developed in the community.  The Whiley build tool allows you to easily manage your dependencies and distribute libraries.</li>
</ul>
{{</section>}}

{{<rawhtml>}}
<script>
 var d = document.getElementById("editor");
 var editor = ace.edit(d);
 editor.setTheme("ace/theme/whiley");
 editor.session.setMode("ace/mode/whiley");      
</script>
{{</rawhtml>}}