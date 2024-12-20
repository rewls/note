# GitHub Flavored Markdown Spec

> GitHub Flavored Markdown Spec Version 0.29-gfm
>
> | Publication date |
> | ---------------- |
> | 2019-04-06       |

- This formal specification is based on the CommonMark Spec by John MacFarlane and licensed under Creative Commons BY-SA.

## 1 Introduction

### 1.1 What is GitHub Flavored Markdown?

- GitHub Flavored Markdown, often shortened as GFM, is the dialect of Markdown that is currently supported for user content on GitHub.com and GitHub Enterprise.

<br>

- This formal specification, based on the CommonMark Spec, defines the syntax and semantics of this dialect.

<br>

- GFM is a strict superset of CommonMark.

- All the features which are supported in GitHub user content and that are not specified on the original CommonMark Spec are hence known as extensions, and highlighted as such.

- While GFM supports a wide range of inputs, it’s worth noting that GitHub.com and GitHub Enterprise perform additional post-processing and sanitization after GFM is converted to HTML to ensure security and consistency of the website.

## 4 Leaf blocks

- This section describes the different kinds of leaf block that make up a Markdown document.

> ### 4.10 Tables (extension)
> 
> - GFM enables the table extension, where an additional leaf block type is available.
> 
> <br>
> 
> - A table is an arrangement of data with rows and columns, consisting of a single header row, a delimiter row separating the header from the data, and zero or more data rows.
> 
> <br>
> 
> - Each row consists of cells containing arbitrary text, in which inlines are parsed, separated by pipes (|).
> 
> - A leading and trailing pipe is also recommended for clarity of reading, and if there’s otherwise parsing ambiguity.
> 
> - Spaces between pipes and cell content are trimmed.
> 
> - Block-level elements cannot be inserted in a table.
> 
> <br>
> 
> - The delimiter row consists of cells whose only content are hyphens (-), and optionally, a leading or trailing colon (`:`), or both, to indicate left, right, or center alignment respectively.
> 
> > ##### Example 198
> >
> > ```markdown
> > | foo | bar |
> > | --- | --- |
> > | baz | bim |
> > ```
> > 
> > ```html
> > <table>
> > <thead>
> > <tr>
> > <th>foo</th>
> > <th>bar</th>
> > </tr>
> > </thead>
> > <tbody>
> > <tr>
> > <td>baz</td>
> > <td>bim</td>
> > </tr>
> > </tbody>
> > </table>
> > ```
> >
> > | foo | bar |
> > | --- | --- |
> > | baz | bim |
> 
> - Cells in one column don't need to match length, though it’s easier to read if they are.
> 
> - Likewise, use of leading and trailing pipes may be inconsistent.
> 
> <br>
> 
> - Include a pipe in a cell’s content by escaping it, including inside other inline spans.
> 
> <br>
> 
> - The table is broken at the first empty line, or beginning of another block-level structure.
> 
> <br>
> 
> - The header row must match the delimiter row in the number of cells.
> 
> - If not, a table will not be recognized.
> 
> <br>
> 
> - The remainder of the table’s rows may vary in the number of cells.
> 
> - If there are a number of cells fewer than the number of cells in the header row, empty cells are inserted.
> 
> - If there are greater, the excess is ignored.
> 
> - If there are no rows in the body, no `<tbody>` is generated in HTML output.

## 5 Container blocks

- A container block is a block that has other blocks as its contents.

- There are two basic kinds of container blocks: block quotes and list items.

- Lists are meta-containers for list items.

<br>

- We define the syntax for container blocks recursively.

- The general form of the definition is:

    - If X is a sequence of blocks, then the result of transforming X in such-and-such a way is a container of type Y with these blocks as its content.

<br>

- So, we explain what counts as a block quote or list item by explaining how these can be generated from their contents.

- This should suffice to define the syntax, although it does not give a recipe for parsing these constructions.

    - A recipe is provided below in the section entitled A parsing strategy.

> ### 5.3 Task list items (extension)
> 
> - GFM enables the `tasklist` extension, where an additional processing step is performed on list items.
> 
> <br>
> 
> - A task list item is a list item where the first block in it is a paragraph which begins with a task list item marker and at least one whitespace character before any other content.
> 
> <br>
> 
> - A task list item marker consists of an optional number of spaces, a left bracket (`[`), either a whitespace character or the letter `x` in either lowercase or uppercase, and then a right bracket (`]`).
> 
> <br>
> 
> - When rendered, the task list item marker is replaced with a semantic checkbox element; in an HTML output, this would be an `<input type="checkbox">` element.
> 
> <br>
> 
> - If the character between the brackets is a whitespace character, the checkbox is unchecked.
> 
> - Otherwise, the checkbox is checked.
> 
> <br>
> 
> - This spec does not define how the checkbox elements are interacted with: in practice, implementors are free to render the checkboxes as disabled or inmutable elements, or they may dynamically handle dynamic interactions (i.e. checking, unchecking) in the final rendered document.
> 
> > ##### Example 279
> >
> > ```markdown
> > - [ ] foo
> > - [x] bar
> > ```
> >  
> > ```html
> > <ul>
> > <li><input disabled="" type="checkbox"> foo</li>
> > <li><input checked="" disabled="" type="checkbox"> bar</li>
> > </ul>
> > ```
> > 
> > - [ ] foo
> > - [x] bar
> 
> - Task lists can be arbitrarily nested.
