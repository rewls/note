# Compare AsciiDoc to Markdown

- The most compelling reason to choose a lightweight markup language for writing is to minimize the number of technical concepts an author must grasp in order to be immediately productive.

- In other words, the goal is to be able to *write without friction*.

- While that's certainly the goal of both AsciiDoc and Markdown, and both are very approachable for newcomers, this page explores why AsciiDoc is a more suitable alternative to Markdown as your content grows and evolves.

## Starting with Markdown

- The most prevalent lightweight markup language is Markdown.

    - At least, Markdown is what you call it at first.

- The main advantage of Markdown lies in its primitive syntax: its manual and cheatsheet are one and the same.

- But this advantage is also its greatest weakness.

<br>

- As soon as authors need something slightly more complex than basic prose (e.g., tables, cross references, footnotes, embedded YouTube videos, etc.), they find themselves resorting to embedded HTML or seeking out more feature-rich implementations.

- Markdown has become a maze of different implementations, termed "flavors", which make a universal definition evasive.

> ##### Note
>
> - The IETF has declared "there is no such thing as "invalid" Markdown." See [This Is Markdown! Or: Markup and Its Discontents](https://datatracker.ietf.org/doc/html/rfc7763#section-1.1).

## Graduating to AsciiDoc

- AsciiDoc presents a more sound alternative.

- The AsciiDoc syntax is more concise than (or at least as concise as) Markdown.

- At the same time, AsciiDoc offers power and flexibility without requiring the use of HTML or "flavors" for essential syntax such as tables, description lists, admonitions (tips, notes, warnings, etc.) and table of contents.

<br>

- It's important to understand that AsciiDoc was initially designed as a plain-text alternative to the DocBook XML schema.

- AsciiDoc isn't stuck in a game of whack-a-mole trying to satisfy publishing needs like Markdown.

- Rather, the AsciiDoc syntax was explicitly designed with the needs of publishing in mind, both print and web.

- If the need arises, you can make full use of the huge choice of tools available for a DocBook workflow using Asciidoctor's DocBook converter.

- That's why mapping to an enterprise documentation format like DocBook remains a key use case for AsciiDoc.

<br>

- And yet, AsciiDoc is simple enough to stand in as a better flavor of Markdown.

- But what truly makes AsciiDoc the right investment is that its syntax was designed to be extended as a core feature.

- This extensibility not only means that AsciiDoc has a lot more to offer, with room to grow, it also fulfills the objective of ensuring your content is maximally reusable.

## Comparison by example

- The following table shows the AsciiDoc syntax as it compares to Markdown.

- Since AsciiDoc supports a broader range of syntax than Markdown, this side-by-side comparison focuses mainly on areas where the syntax overlaps.

<br>

- *A selection of AsciiDoc language features compared to Markdown*

##### Bold (constrained)

```markdown
**bold**
```

---

```asciidoc
*bold*
```

##### Bold (unconstrained)

```markdown
**b**old
```

---

```asciidoc
**b**old
```

##### Italic (constrained)

```markdown
*italic*
```

---

```asciidoc
_italic_
```

##### Italic (unconstrained)

n/a

---

```asciidoc
__i__talic
```

##### Monospace (constrained)

```markdown
`monospace`
```

---

```asciidoc
`monospace`
```

##### Monospace (unconstrained)

```markdown
`m`onospace
```

---

```asciidoc
``m``onospace
```

##### Literal monospace

```markdown
`http://localhost:8080`
`/issue/{id}`
```

---

```asciidoc
`+http://localhost:8080+`
`+/issue/{id}+`
```

##### Link with label

```markdown
[Asciidoctor](https://asciidoctor.org)
```

---

```asciidoc
https://asciidoctor.org[Asciidoctor]
```

##### Relative link

```markdown
[user guide](user-guide.html)
```

---

```asciidoc
link:user-guide.html[user guide]
xref:user-guide.adoc[user guide]
```

##### File link

```markdown
[get the PDF]({% raw %}{{ site.url }}{% endraw %}/assets/mydoc.pdf)
```

---

```asciidoc
link:{site-url}/assets/mydoc.pdf[get the PDF]
```

##### Cross reference

```markdown
See [Usage](#_usage).

<h2 id="_usage">Usage</h2>
```

---

```asciidoc
See <<_usage>>.

== Usage
```

##### Block ID (aka anchor)

```markdown
<h2 id="usage">Usage</h2>
```

---

```asciidoc
[#usage]
== Usage
```

##### Inline anchor

n/a

---

```asciidoc
. [[step-1]]Download the software
```

##### Inline image w/ alt text

```markdown
![Logo](/images/logo.png)
```

---

```asciidoc
image:logo.png[Logo]
```

##### Block image w/ alt text

n/a

---

```asciidoc
image::logo.png[Logo]
```

##### Section heading*

```markdown
## Heading 2
```

---

```asciidoc
== Heading 2
```

##### Blockquote*

```markdown
> Quoted text.
>
> Another paragraph in quote.
```

---

```markdown
____
Quoted text.

Another paragraph in quote.
____
```

##### Literal block

```markdown
    $ gem install asciidoctor
```

---

- Example 1. Indented (by 1 or more spaces)

    ```asciidoc
     $ gem install asciidoctor
    ```

- Example 2. Delimited

    ```asciidoc
    ....
    $ gem install asciidoctor
    ....
    ```

##### Code block*

```markdown
```java
public class Person {
  private String name;
  public Person(String name) {
    this.name = name;
  }
}
```
```

---

```asciidoc
[source,java]
----
public class Person {
  private String name;
  public Person(String name) {
    this.name = name;
  }
}
----
```

##### Unordered list

```markdown
* apples
* orange
  * temple
  * navel
* bananas
```

---

```asciidoc
* apples
* oranges
** temple
** navel
* bananas
```

##### Ordered list

```markdown
1. first
2. second
3. third
```

---

```asciidoc
. first
. second
. third
```

##### Thematic break (aka horizontal rule)*

```markdown
***

* * *

---

- - -

___

_ _ _
```

---

```asciidoc
'''
```

##### Typographic quotes (aka "smart quotes")

Enabled through an extension switch, but offer little control in how they are applied.

---

```asciidoc
The `'90s popularized a new form of music known as "`grunge`" rock.
It'll turn out to have an impact that extended well beyond music.
```

##### Document header

- Example 3. Slapped on as "front matter"

    ```markdown
    ---
    layout: docs
    title: Writing posts
    prev_section: defining-frontmatter
    next_section: creating-pages
    permalink: /docs/writing-posts/
    ---
    ```

---

- Example 4. Native support!

    ```asciidoc
    = Writing posts
    :page-layout: base
    :showtitle:
    :prev_section: defining-frontmatter
    :next_section: creating-pages
    ```

##### Admonitions

n/a

---

```asciidoc
TIP: You can add line numbers to source listings by adding the word `numbered` in the attribute list after the language name.
```

##### Sidebars

n/a

---

```asciidoc
.Lightweight Markup
****
Writing languages that let you type less and express more.
****
```

##### Block titles

n/a

---

```asciidoc
.Grocery list
* Milk
* Eggs
* Bread
```

##### Includes

n/a

---

```asciidoc
include::intro.adoc[]
```

##### URI reference

```markdown
Go to the [home page][home].

[home]: https://example.org
```

---

```asciidoc
:home: https://example.org

Go to the {home}[home page].
```

##### Custom CSS classes

n/a

---

```
[.path]_Gemfile_
```

- * Asciidoctor also supports the Markdown syntax for this language feature.

<br>

- You can see that AsciiDoc has the following advantages over Markdown:

    - AsciiDoc uses the same number of markup characters or less when compared to Markdown in nearly all cases.

    - AsciiDoc uses a consistent formatting scheme (i.e., it has consistent patterns).

    - AsciiDoc can handle all permutations of nested inline (and block) formatting, whereas Markdown often falls down.

    - AsciiDoc handles cases that Markdown doesn't, such as a proper approach to inner-word markup, source code blocks and block-level images.

> ##### Note
>
> - Certain Markdown flavors, such as Markdown Extra, support additional features such as tables and description lists.
>
> - However, since these features don't appear in "plain" Markdown, they're not included in the comparison table.
>
> - But they're supported natively by AsciiDoc.

- Asciidoctor, which is used for converting AsciiDoc on GitHub and GitLab, emulates some of the common parts of the Markdown syntax, like headings, blockquotes and fenced code blocks, simplifying the migration from Markdown to AsciiDoc.

- For details, see Markdown compatibility.
