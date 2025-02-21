---
title: markdown syntax
author: ramraid
date: 2024-02-12 20:30:00 +0800
categories: [Blogging, Markdown]
tags: [Markdown]
math: true
image:
    path: /assets/img/cat.png
    alt: 블로그 이사 :/
render_with_liquid: false
pin: false
---

# markdown syntax

블로그 이사 기념 markdown syntax recap

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
| Company                      | Contact          | Country |
| :--------------------------- | :--------------- | ------: |
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    |      UK |
| Magazzini Alimentari Riuniti | Giovanni Rovelli |   Italy |

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

![cat](/assets/img/cat.png)

[^footnote]: The first
[^fn-nth-2]: The second