---
title: "Authors Guide for Git graphs"
permalink: /author-guide/
---
{% include mermaid.html %}

## Mermaid Examples

[Mermaid](https://mermaid-js.github.io/mermaid/#/) is a JavaScript library that can be used
to write various graphs and flow-charts within Markdown and render them on a website. 

To enable Mermaid support add the following line to any page:
{% comment %}
As you are reading the source-code:
Just add the  `{% include mermaid.html %}` and not the `{% raw %}` and `{% endraw %}`.
{% endcomment %}
```
{% raw %}{% include mermaid.html %}{% endraw %}
```
Then mermaid graphs can be used as shown below.

### Git Graph

```
<div class="mermaid">
gitGraph:
options
{
    "nodeSpacing": 100,
    "nodeRadius": 10
}
end
commit
branch newbranch
checkout newbranch
commit
commit
checkout master
commit
commit
merge newbranch
</div>
```

<div class="mermaid">
gitGraph:
options
{
    "nodeSpacing": 100,
    "nodeRadius": 10
}
end
commit
branch newbranch
checkout newbranch
commit
commit
checkout master
commit
commit
merge newbranch
</div>

### Flow Chart

```
<div class="mermaid">
graph LR
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
</div>
```

<div class="mermaid">
graph LR
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
</div>

{% include links.md %}
