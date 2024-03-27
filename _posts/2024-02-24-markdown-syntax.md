---
title: markdown syntax
author: ramraid
date: 2024-02-24 20:30:00 +0800
categories: [Blogging]
tags: [writing]
toc: true
comments: true
math: false
mermaid: false
image:
    path: /assets/img
    alt: nothing around to show :/
# render_with_liquid: false
pin: false
---

# markdown syntax

## Headings

```Markdown
# Heading - 1
## Heading - 2
### Heading - 3
#### Heading - 4
```

## Lists

### Ordered list
1. codes
2. games
3. coffee

### Unordered list
- Chapter
    - Section
        - Paragraph

### TODO list
- [ ] Study
    - [x] C++
    - [x] Algorithm
    - [ ] Unreal Engine

### Description list
C++
: the best language.

Unreal Engine
: now studying

## Block Quote

> this is the _block quote_.

## Prompts

> this is a 'tip'
{: .prompt-tip }

> this is a 'info'
{: .prompt-info }

> this is a 'warning'
{: .prompt-warning }

> this is a 'danger'
{: .prompt-danger }

## Tables
| Games                   | Genre  |
| :---------------------- | :----- |
| Legend of Zelda         | RPG    |
| Helldivers 2            | TPS    |
| Doom                    | FPS    |

## Links
<https://ramraid319.github.io>

## Footnote
click me ---> [^footnote], click me, too ---> [^fn-nth-2].

## Mathmatics

$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

## Codes

```yaml
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG]     # TAG names should always be lowercase
---
```

![cat](cat.png)