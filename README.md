# sample--hello

<a href="https://www.facebook.com/" target="_blank">Go to application</a> 

%md <a href="https://google.com" target="_blank">google link</a>

<a href="https://www.google.com/" target="_blank">Google</a>

<p>Check out <a href="https://www.freecodecamp.org/" target="_blank">freeCodeCamp</a>.</p>

[go](http://stackoverflow.com){:target="_blank"}

[go](http://stackoverflow.com){:target="_blank" rel="noopener"}

<a href="doc:introduction" target="_blank">Introduction</a>

<a href="https://www.google.com/" target="_blank">Google</a>

[my link](https://www.google.com)[newtab]


<a href="example.com" target="_blank">New Tab</a>

sed -i 's|href="http|target="_blank" href="http|g' index.html

const linkRenderer = renderer.link;
renderer.link = (href, title, text) => {
  const html = linkRenderer.call(renderer, href, title, text);
  return html.replace(/^<a /, '<a target="_blank" rel="nofollow" ');
};
  
  <p><red> red color markdown text</red>
  
  <style>
red { color: red }
yellow { color: yellow }
</style>

<red> red color markdown text</red>
<yellow> red color markdown text</yellow>
