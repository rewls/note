# Syntax

## Overview

### Philosophy

- Markdown is intended to be as easy-to-read and easy-to-write as is feasible.

<br>

- Readability, however, is emphasized above all else.

- A Markdown-formatted document should be publishable as-is, as plain text, without looking like it's been marked up with tags or formatting instructions.

- While Markdown's syntax has been influenced by several existing text-to-HTML filters.

- The single biggest source of inspiration for Markdown's syntax is the format of plain text email.

<br>

- To this end, Markdown's syntax is comprised entirely of punctuation characters, which punctuation characters have been carefully chosen so as to look like what they mean.

### Inline HTML

- Markdown's syntax is intended for one purpose: to be used as a format for *writing* for the web.

<br>

- Markdown is not a replacement for HTML, or even close to it.

- Its syntax is very small, corresponding only to a very small subset of HTML tags.

- The idea is *not* to create a syntax that make it easier to insert HTML tags.

- In my opinion, HTML tags are already easy to insert.

- The idea for Markdown is to make it easy to read, write, and edit prose.

- HTML is a *publishing* format; Markdown is a *writing* format.

- Thus, Markdown's formatting syntax only addresses issues that can be conveyed in plain text.

<br>

- For any markup that is not covered by Markdown's syntax, you simply use HTML itself.

- There's no need to preface it or delimit it to indicate that you're switching from Markdown to HTML; you just use the tags.

<br>

- The only restrictions are that block-level HTML elements -- must be separated from surrounding content by blank lines, and the start and end tages of the block should not be indented with tabs or spaces.

- Markdown is smart enough not to add extra `<p>` tags around HTML block-level tags.

<br>

- Note that Markdown formatting syntax is not processed within block-level HTML tags.

<br>

- Span-level HTML tags can be used anywhere in a Markdown paragraph, list item, or header.

<br>

- Unlike block-level HTML tags, Markdown syntax *is* processed within span-level tags.

### Automatic escaping for special characters

- In HTML, there are two characters that demand special treatment: `<` and `&`.

- Left angle brackets are used to start tags; ampersands are used to denote HTML entities.

- If you want to use them as literal characters, you must escape them as entities, e.g. `&lt;`, and `&amp;`.

<br>

- Markdown allows you to use these characters naturally, taking care of all the necessary escaping for you.

- If you use an ampersand as part of an HTML entity, it remains unchanged.

<br>

- So, if you want to include a copyright symbol in your article, you can write:

    ```markdown
    &copy;
    ```

<br>

- However, inside Markdown code spans and blocks, angle brackets and ampersands are encoded automatically.

## Block Elements

###  Paragraphs and line breaks

- A paragraph is simply one or more consecutive lines of text, separated by one or more blank lines.

    - A blank line is any line that looks like a blank line -- a line containing nothing but spaces or tabs is considered blank.

- Normal paragraphs should not be indented with spaces or tabs.

<br>

- The implication of the "one or more consecutive lines of text" rule is that Markdown supports "hard-wrapped" text paragraphs.

<br>

- When you *do* want to insert a `<br />` break tag using Markdown, you end a line with two or more spaces, then type return.

- Yes, this takes a tad more effort to create a `<br />`.

- Markdown's email-style blockquoting and multi-paragraph list items work best -- and look better -- when you format them with hard breaks.

### Headers

- Markdown supports two styles of headers, Setext and atx.

- Setext-style headers are "underlined" using equal signs (for first-level headers) and dashes (for second-level headers).

- For example:

    ```markdown
    This is an H1
    =============

    This is an H2
    -------------
    ```

<br>

- Any number of underlining `=`'s or `-`'s will work.

<br>

- Atx-style headers use 1-6 hash characters at the start of the line, corresponding to header levels 1-6.

    ```markdown
    # This is an H1
    
    ## This is an H2
    
    ###### This is an H6
    ```

- Optionally, you may "close" atx-style headers.

- This is purely cosmetic -- You can use this if you think it looks better.

- The closing hashes don't even need to match the number of hashes used to open the header.

    - The number of opening hashes determines the header level.

    ```markdown
    # This is an H1 #

    ## This is an H2 ##

    ### This is an H3 ######
    ```

### Blockquotes

- Markdown uses email-style `>` characters for blockquoting.

- It looks best if you hard wrap the text and put a `>` before every line.

    ```markdown
    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    > consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    > Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
    >
    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    > id sem consectetuer libero luctus adipiscing.
    ```

- Makdown allows you to be lazy and only put the `>` before the first line of a hard-wrapped paragraph:

    ```markdown
    > This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
    consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
    Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
    id sem consectetuer libero luctus adipiscing.
    ```

- Blockquotes can be nested by adding additional levels of `>`:

    ```markdown
    > This is the first level of quoting.
    >
    > > This is nested blockquote.
    >
    > Back to the first level.
    ```

- Blockquotes can contain other Markdown elements.

### Lists

- Markdown supports ordered (numbered) and unordered (bulleted) lists.

<br>

- Unordered lists use asterisks, pluses, and hyphens -- interchangeably -- as list markers:

    ```markdown
    *   Red
    *   Green
    *   Blue
    ```

- Ordered lists use numbers followed by periods:

    ```markdown
    1.  Bird
    2.  McHale
    3.  Parish
    ```

- It's important to note that the actual numbers you use to mark the list have no effect on the HTML output Markdown produces.

- The HTML Markdown produces from the above list is:

    ```html
    <ol>
    <li>Bird</li>
    <li>McHale</li>
    <li>Parish</li>
    </ol>
    ```

- If you do use lazy list numbering, however, you should still start the list with the number 1.

- At some point in the future, Markdown may support starting ordered lists at an arbitrary number.

<br>

- List markers typically start at the left margin, but may be intended by up to three spaces.

- List markers must be followed by one or more spaces or a tab.

<br>

- To make lists look nice, you can wrap items with hanging indents:

    ```markdown
    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
        Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
        viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
        Suspendisse id sem consectetuer libero luctus adipiscing.
    ```

- But if you want to be lazy, you don't have to:

    ```markdown
    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
    ```

- If list items are separated by blank lines, Markdown will wrap the items in `<p>` tags in the HTML output.

- For example, this input:

    ```markdown
    *   Bird
    *   Magic
    ```

    - will turn into:

    ```html
    <ul>
    <li>Bird</li>
    <li>Magic</li>
    </ul>
    ```

- But this:

    ```markdown
    *   Bird

    *   Magic
    ```

    - will turn into:
    
    ```html
    <ul>
    <li><p>Bird</p></li>
    <li><p>Magic</p></li>
    </ul>
    ```

- List items may consist of multiple paragraphs.

- Each subsequent paragraph in a list item must be intended by either 4 spaces or one tab:

    ```markdown
    1.  This is a list item with two paragraphs. Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.

        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.

    2.  Suspendisse id sem consectetuer libero luctus adipiscing.
    ```

- It looks nice if you indent every line of the subsequent paragraphs, but here again, Markdown will allow you to be lazy:

    ```markdown
    *   This is a list item with two paragraphs.

        This is the second paragraph in the list item. You're
    only required to indent the first line. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

    *   Another item in the same list.
   ```

- To put a block quote within a list item, the blockquote's `>` delimiters need to be indented:

    ```markdown
    *   A list item with a blockquote:

        > This is a blockquote
        > inside a list item.
    ```

- To put a code block within a list item, the code block needs to be indented *twice* -- 8 spaces or two tabs:

    ```markdown
    *   A list item with a code block:

        <code goes here>
    ```

- Markdown will generate:

    ```html
    <p>This is a normal paragraph:</p>

    <pre><code>This is a code block.
    </code></pre>
    ```

- One level of indentation -- 4 spaces or 1 tab -- is removed from each line of the code block.

- A code block continues until it reaches a line that is not indented (or the end of the article).

<br>

- Within a code block, ampersands and angle brackets are automatically converted into HTML entities.

- This makes it very easy to include example HTML source code using Markdown.

- Regular Markdown syntax is not processed within code blocks.

### Horizontal rules

- You can produces a horizontal rule tag (`<hr />`) by placing three or more hyphens, asterisks, or underscores on a line by themselves.

- If you wish, you may use spaces between the hyphens or asterisks.

## Span elements

### Links

- Markdown supports two style of links: *inline* and *reference*.

<br>

- In both styles, the link text is delimited by [square brackets].

<br>

- To create an inline link, use a set of regular parentheses immediately after the link text's closing square bracket.

- Inside the parentheses, put the URL where you want the link to point, along with an *optional* title for the link, surrounded in quotes.

- For example:

    ```markdown
    This is [an example](http://example.com/ "Title") inline link.

    [This link](http://example.net/) has no title attribute.
    ```

    - will produce:

    ```markdown
    <p>This is <a href="http://example.com/" title="Title">
    an example</a> inline link.</p>

    <p><a href="http://example.net/">This link</a> has no
    title attribute.</p>
    ```

- If you're referring to a local resource on the same server, you can use relative paths.

- Reference-style links use a second set of square brackets, inside which you place a label of your choosing to identify the link:

    ```markdown
    This is [an example][id] reference-style link.
    ```

- You can optionally use a space to separate the sets of brackets.

- Then, anywhere in the document, you define your link label like this, on a line by itself:

    ```markdown
    [id]: http://example.com/  "Optional Title Here"
    ```

- That is:

    - Square brackets containing the link identifier (optionally indented from the left margin using up to three spaces);

    - followed by a colon;

    - followed by one or more spaces (or tabs);

    - followed by the URL for the link

    - optionally followed by a title attribute for the link, enclosed in double or single quotes, or enclosed in parentheses.

- The link URL may, optionally, be surrounded by angle brackets.

- You can put the title attribute on the next line and use extra spaces or tabs for padding, which tends to look better with longer URLs.

- Link definitions are only used for creating links during Markdown processing, and are stripped from your document in the HTML output.

<br>

- Link definition names may consist of letters, numbers, spaces, and punctuation -- but they are *not* case sensitive.

- The *implicit link name* shortcut allows you to omit the name of the link, in which case the link text itself is used as the name.

- Link names may contain spaces.

- Link definitions can be placed anywhere in our Markdown document.

- I tend to put them immediately after each paragraph in which they're used, but if you want, you can put them all at the end of your document, sort of like footnotes.

<br>

- The point of reference-style links is not that they're easier to write.

- The point is that with reference-style links, your document source is vastly more readable.

### Emphasis

- Markdown treats asterisks and underscores as indicators of emphasis.

- Text wrapped with one `*` or `_` will be wrapped with an HTML `<em>` tag; double `*`'s or `_`'s will be wrapped with an HTML `<strong>` tag.

- You can use whichever style you prefer; the lone restriction is that the same character must be used to open and close an emphasis span.

<br>

- But if you surround an `*` or `_` with spaces, it'll be treated as a literal asterisk or underscore.

<br>

- To produce a literal asterisk or underscore at a position where it would otherwise be used as an emphasis delimiter, you can backslash escape it:

    ```markdown
    \*this text is surrounded by literal asterisks\*
    ```

### Code

- To indicate a span of code, wrap it with backtick quotes (`` ` ``).

- Unlike a pre-formatted code block, a code span indicates code within a normal paragraph.

- For example:

    ```markdown
    Use the `printf()` function.
    ```

- will produce:

    ```markdown
    <p>Use the <code>printf()</code> function.</p>
    ```

- To include a literal backtick character within a code span, you can use multiple backticks as the opening and closing delimiters

- The backtick delimiters surrounding a code span may include spaces -- one after the opening, one before the closing.

- This allows you to place literal backtick characters at the beginning or end of a code span.

### Images

- Markdown uses an image syntax that is intended to resemble the syntax for links, allowing for two styles: *inline* and *reference*.

- Inline image syntax looks like this:

    ```markdown
    ![Alt text](/path/to/img.jpg)

    ![Alt text](/path/to/img.jpg "Optional title")
    ```

- That #include <stdio.h>

    - An exclamation mark: `!`;

    - followed by a set of square brackets, containing the `alt` attribute text for the image;

    - followed by a set of parentheses, containing the URL or path to the image, and an optional `title` attribute enclosed in double or single quotes.

- Reference-style image syntax looks like this:

    ```markdown
    ![Alt text][id]
    ```

    - where "id" is the name of a defined image reference.

- Image references are defined using syntax identical to link references.

- As of this writing, Markdown has no syntax for specifying the dimensions of an image; if this is important to you, you can simply use regular HTML `<img>` tags.

## Miscellaneous

### Automatic links

- Markdown supports a shortcut style for creating "automatic" links for URLs and email addresses: simply surround the URL or email address with angle brackets.

- What this means is that if you want to show the actual text of a URL or email address, and also have it be a clickable link, you can do this:

    ```markdown
    <http://example.com/>
    ```

- Markdown will turn this into:

    ```markdown
    <a href="http://example.com/">http://example.com/</a>
    ```

- Automatic links for email addresses work similarly, except that Markdown will also perform a bit of randomized decimal and hex entity-encoding to help obscure your address from address-harvesting spambots.

- This sort of entity-encoding trick will indeed fool many, if not most, address-harvesting bots, but it definitely won't fool all of them.

### Backslash escapes

- Markdown allows you to use backslash escapes to generate literal characters which would otherwise have special meaning in Markdown's formatting syntax.

- Markdown provides backslash escapes for the following characters:

    ```
    \   backslash
    `   backtick
    *   asterisk
    _   underscore
    {}  curly braces
    []  square brackets
    ()  parentheses
    #   hash mark
    +   plus sign
    -   minus sign (hyphen)
    .   dot
    !   exclamation mark
    ```
