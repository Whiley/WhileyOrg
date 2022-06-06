---
title: "Install"
date: 2017-10-13T20:31:39-05:00
draft: false
---

{{< section>}}
<div class="column">
<h1>Install</h1>
</div>
{{</section>}}

{{<section>}}
<div class="column">

Whiley is currently written in a combination of <a
href="https://rust-lang.org/">Rust</a> and <a
href="https://www.java.com/">Java</a>.  This is for legacy reasons,
since the compiler was originally written in Java and is now being
migrated to Rust.  <b>As such you need to have Java installed on your
machine.</b>

The simplest way to install Whiley is through Cargo (see instructions
for installing via <code>rustup</code> <a
href="https://www.rust-lang.org/tools/install">here</a>).  To install
Whiley, run <code>cargo</code> as follows:

<pre>> cargo install whiley</pre>

This will download and compile the latest version of Whiley (note this
also requires <code>libssl-dev</code> is installed).  You can then
test your installation as follows:

<pre>> wy</pre>

You should then see information about the various commands you can run
(e.g. <code>build</code>).  See the <a href="/learn">getting started</a>
guide for what to do next.

</div>
{{</section>}}

<!--
{{<section class="alternate">}}
<div class="column">
<h2>Linux</h2>

(precompiled binaries for linux)

</div>

<div class="column">
<h2>MacOs</h2>

(precompiled binaries for linux)

</div>

<div class="column">
<h2>Windows</h2>

(precompiled binaries for linux)

</div>

{{</section>}}

{{<section>}}
<div class="column">
<h2>Downloads</h2>
</div>
{{</section>}}
-->