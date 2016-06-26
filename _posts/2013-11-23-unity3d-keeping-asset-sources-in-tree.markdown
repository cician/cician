---
layout: post
title:  "Unity3D: keeping asset sources in the tree"
date:   2013-11-23 10:35:00 +0100
categories: updates gamedev Unity3D
---
It's advisable to keep source files for the assets (ex.: .ps, .max, .blend) near
the final ones you actually want Unity to import because it's a lot easier to
keep things organized this way and work with Version Control Systems. Folks will
tell you to keep a mirror structure outside of assets folder, which is the exact
opposite.

![Do not want!]({{ site.baseurl }}/files/do-not-want.jpg)

So here's the trick: Unity doesn't import files and folders that are hidden or
have the name starting with a dot. Naming files with a starting dot is better in
my opinion. Git for example doesn't store the hidden attribute, and other VCSes
probably don't as well.

You can do something like this:
{% raw %}
<span style="color: #999999; font-family: Courier New, Courier, monospace;">.monkey.max &nbsp; &nbsp; &nbsp; &nbsp; &lt;- source file, not imported</span><br />
<span style="font-family: Courier New, Courier, monospace;">monkey.fbx &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&lt;- imported normally</span><br />
<span style="color: #999999; font-family: Courier New, Courier, monospace;">.monkey_diffuse.psd &lt;- source file, not imported</span><br />
<span style="font-family: Courier New, Courier, monospace;">monkey_diffuse.png &nbsp;&lt;- imported normally</span><br />
{% endraw %}

or

{% raw %}
<span style="font-family: Courier New, Courier, monospace;">monkey.fbx &nbsp; &nbsp; &nbsp; &nbsp; &lt;- imported normally</span><br />
<span style="font-family: Courier New, Courier, monospace;">monkey_diffuse.png &lt;- imported normally</span><br />
<span style="color: #999999; font-family: Courier New, Courier, monospace;">.source &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&lt;- entire folder not imported</span><br />
<span style="color: #999999; font-family: Courier New, Courier, monospace;">.source/monkey.max</span><br />
<span style="color: #999999; font-family: Courier New, Courier, monospace;">.source/monkey_diffuse.psd</span><br />
{% endraw %}

The second structure can be better with many files. Windows explorer won't let
you name a directory this way though (THANK YOU MICROSOFT!). Create or rename it
and write ".source." (with final dot added), it will name it ".source" stripping
the final dot. Tested on Windows 7, don't ask me why it's like this.

Hopefully it will save you some headaches.
