---
draft: false
banner: "A language for writing correct software!"
---
{{<section class="banner">}}

{{% column %}}
# Whiley
### Creating high integrity software at scale.
{{<button url="window.location.href='learn'" text="Get Started!!" >}}
{{% /column %}}

{{% column %}}
```Whiley
/**
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
```
{{% /column %}}
{{</section>}}

{{<section>}}
{{% column %}}
### Reliability
Whiley employs state-of-the-art techniques for ensuring your
**software is correct**.  You can specify functions using
[preconditions](https://en.wikipedia.org/wiki/Precondition") and
[postconditions](https://en.wikipedia.org/wiki/Postcondition), and
then [statically
verify](https://en.wikipedia.org/wiki/Formal_verification)( your
implementation meets its specification.
{{%/column %}}

{{% column %}}
### Open Source
Whiley is an independently developed open source project and is free
to use.  Join our community on our [Discord
channel](https://discord.com/channels/825109901352632331/825109901352632334),
follow us on [Twitter](https://twitter.com/WhileyLang) and contribute
to the code on [GitHub](http://github.com/Whiley).  
{{%/column %}}

{{% column %}}
### Flexibility
Whiley supports
[functional](https://en.wikipedia.org/wiki/Functional_programming) and
[imperative](https://en.wikipedia.org/wiki/Imperative_programming)
programming without being opinionated.  Whiley can be used to develop
web applications, smart contracts, embedded systems and more.  
{{%/column %}}
{{</section>}}

{{<section class="alternate">}}
{{% column %}}
{{<youtube id="MLcNhc27Ghw">}}
{{%/column %}}

{{% column %}}
{{<youtube id="yYGEcyCHiZk">}}
{{% /column %}}

{{% column %}}
{{<youtube id="1KfZH_jjrG4">}}
{{% /column %}}

{{< /section>}}

{{< section>}}
{{% column %}}

### Features

   * **Specification.** Unlike most other programming languages, Whiley provides first-class support for specifying functions using preconditions and postconditions.

   * **Static Typing.** Whiley is a [statically typed](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) programming language which employs [type inference](https://www.google.com/search?channel=fs&client=ubuntu&q=type+inference) and [flow typing](https://en.wikipedia.org/wiki/Flow-sensitive_typing) for ease of use.

   * **Static Verification.** Whiley supports static verification technology to give sophisticated support for finding software errors.

   * **Automated Testing.** Whiley supports automated testing (in the style of QuickCheck) to quickly check for errors and other problems.

   * **Package Management.** Whiley has a small but growing selection of packages developed in the community.  The Whiley build tool allows you to easily manage your dependencies and distribute libraries.
   
{{% /column %}}
{{</section>}}

{{<rawhtml>}}
<script>
 var d = document.getElementById("editor");
 var editor = ace.edit(d);
 editor.setTheme("ace/theme/whiley");
 editor.session.setMode("ace/mode/whiley");      
</script>
{{</rawhtml>}}
