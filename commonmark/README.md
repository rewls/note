# CommonMark

- A strongly defined, highly compatible specification of Markdown

## Why is CommonMark needed?

- John Gruber's canonical description of Markdown's syntax does not specify the syntax unambiguously.

<br>

- In the absence of a spec, early implementers consulted the original Markdown.pl code to resolve these ambiguities.

- But Markdown.pl was quite buggy, and gave manifestly bad results in many cases, so it was not a satisfactory replacement for a spec.

- Markdown.pl was last updated December 17th, 2004.

<br>

- Because there is no unambiguous spec, implementations have diverged considerably over the last 10 years.

- As a result, users are often surprised to find that a document that renders one way on one system (say, a GitHub wiki) renders differently on another (say, converting to docbook using Pandoc).

- To make matters worse, because nothing in Markdown counts as a “syntax error,” the divergence often isn't discovered right away.

<br>

- There's no standard test suite for Markdown; MDTest is the closest thing we have.

- The only way to resolve Markdown ambiguities and inconsistencies is Babelmark, which compares the output of 20+ implementations of Markdown against each other to see if a consensus emerges.

<br>

- We propose a **standard, unambiguous syntax specification for Markdown**, along with a **suite of comprehensive tests** to validate Markdown implementations against this specification.

- We believe this is necessary, even essential, for the future of Markdown.

<br>

- That's what we call **CommonMark**.

## Who are you today?

- We're a group of Markdown fans continually working toward the vision of CommonMark -- a standard, interoperable and testable version of Markdown.

## Who were you in 2014, when this started?

- We're a group of Markdown fans who either work at companies with industrial scale deployments of Markdown, have written Markdown parsers, have extensive experience supporting Markdown with end users -- or all of the above.

## Where can I find it?

- `spec.commonmark.org`: The CommonMark specification.

## When is the spec final?

- The current version of the CommonMark spec is quite robust after many years of public feedback.

<br>

- There are currently CommonMark implementations for dozens of programming languages, and the following sites and projects have adopted CommonMark:

    - GitHub

    - GitLab

    - Reddit

    - Qt

    - Stack Overflow / Stack Exchange
