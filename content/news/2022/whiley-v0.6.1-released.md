---
date: 2022-06-27
title: "Whiley v0.6.1 Released!"
draft: true
---

* **Improved Verification**.  Verification in Whiley continues to get stronger with further improvements to the Boogie backend (see [this post](https://whileydave.com/2022/05/31/whiley-gets-rusty/) and [our paper](https://whileydave.com/publications/pug22_jar/) for more info).  The Boogie backend is now the default verification tool chain and passes >95% of tests.

* **Command-Line Tool** ([Repo](https://github.com/Whiley/WhileyBuildTool)).  The command-line tool `wy` for building and verifying Whiley programs is now written in Rust.  In essence, this provides a wrapper around the existing Java components (see [this post](https://whileydave.com/2022/05/31/whiley-gets-rusty/) for more).  This also adds support for the commands `clean` ({{<issue id="1092">}}) and `init` ({{<issue id="26" repo="WhileyBuildTool">}}), amongst other things.

* **Old Syntax** ({{<issue id="1096">}}).

* **Unsafe Syntax** ({{<issue id="1093">}}).

* **Property Syntax** ({{<issue id="1102">}}).  Along with `if` expression syntax {{<issue id="1151">}}, and preconditions for properties {{<issue id="1157">}}.

* **Test File Format** ({{<issue id="978">}}).  Enabled specific tests for incremental compilation {{<issue id="1149">}}

* **Exponentiation Operator** ({{<issue id="1124">}}).

* **Array/Record Update Operator** ({{<issue id="1129">}}).

* **Bug Fixes** (e.g. {{<issue id="1132">}}, {{<issue id="1142">}}, {{<issue id="1128">}}, {{<issue id="1120">}}, {{<issue id="1103">}}, {{<issue id="1101">}}, {{<issue id="1097">}}, {{<issue id="1098">}}).  As usual there have been plenty of bug fixes, and I've only included a sample of them to the left.

