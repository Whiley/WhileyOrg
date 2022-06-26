---
title: "Install"
date: 2017-10-13T20:31:39-05:00
draft: false
---

{{< section >}}
{{% column %}}

# Install

----

Whiley is currently written in a combination of
[Rust]("https://rust-lang.org/") and [Java](https://www.java.com/").
This is for legacy reasons, since the compiler was originally written
in Java and is now being migrated to Rust.  <b>As such you need to
have Java installed on your machine.</b>

The simplest way to install Whiley is through Cargo (see instructions
for installing via `rustup`
[here](https://www.rust-lang.org/tools/install")).  To install Whiley,
run `cargo` as follows:

```
> cargo install whiley
```

This will download and compile the latest version of Whiley (note this
also requires `libssl-dev` is installed).  You can then test your
installation as follows:

```
> wy
```

You should then see information about the various commands you can run
(e.g. `build`).  See the [getting started](/learn) guide for what to do next.

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

----

{{% /column %}}
{{< /section >}}
