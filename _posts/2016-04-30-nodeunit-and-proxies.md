---
layout: post
title: Nodeunit and Proxies
type: post
status: publish
published: true
---

With [ES6](https://en.wikipedia.org/wiki/ECMAScript#6th_Edition) in javascript we get a lot of cool things to make it a proper programming language, fun stuff like [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy).

Recently I found a nice use for Proxies when writing tests however the [nodeunit](https://github.com/caolan/nodeunit) runner doesn't support the [--harmony-proxies](https://www.npmjs.com/package/harmony-proxy) parameter a small runner was created to allow us to run tests with working Proxy support. Just create a small script that looks something like this.
{% highlight javascript %}
const reporter = require('nodeunit').reporters.minimal;
let args = process.argv;
args.splice(0,2);
reporter.run(args);
{% endhighlight %}
And invoke it using:  
`node --harmony-proxies runtests.js $(find ./tests -name \*.js)` 