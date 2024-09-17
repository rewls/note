# Supported Functions

- This is a list of TeX function supported by KaTeX.

- It is sorted into logical groups.

- There is a similar Support Table, sorted alphabetically, that lists both supported and un-supported functions.

## Accents

|Syntax|Result|
|-|-|
|`a'`|$a'$|
|`a''`|$a''$|
|`\bar{y}`|$\bar{y}$|
|`\hat{\theta}`|$\hat{\theta}$|
|`\tilde{a}`|$\tilde{a}$|
|`\vec{F}`|$\vec{F}$|
|`\overline{AB}`|$\overline{AB}$|

## Delimiters

|Syntax|Result|
|-|-|
|`()`|$()$|
|`[]`|$[]$|
|`\{\}`|$\{\}$|
|`\|`|$\|$|
|`\lvert\rvert`|$\lvert\rvert$|
|`\lang\rang`|$\lang\rang$|
|`\lparen\rparen`|$\lparen\rparen$|
|`\lbrack\rbrack`|$\lbrack\rbrack$|
|`\lbrace\rbrace`|$\lbrace\rbrace$|
|`\langle\rangle`|$\langle\rangle$|
|`\lt\gt`|$\lt\gt$|
|`\left.\right.`|$\left.\right.$|
|`\lceil\rceil`|$\lceil\rceil$|
|`\lfloor\rfloor`|$\lfloor\rfloor$|

### Delimiter Sizing

|Syntax|Result|
|-|-|
|`\left(\middle\|\right)`|$\left(\middle\|\right)$|
|`\big(`|$\big($|
|`\Big(`|$\Big($|
|`\bigg(`|$\bigg($|
|`\Bigg(`|$\Bigg($|

## Environments

```tex
\begin{matrix}
    a & b \\
    c & d
\end{matrix}
```

$$
\begin{matrix}
    a & b \\
    c & d
\end{matrix}
$$

```tex
\begin{pmatrix}
    a & b \\
    c & d \\
\end{matrix}
```

$$
\begin{pmatrix}
    a & b \\
    c & d \\
\end{pmatrix}
$$

```tex
\begin{vmatrix}
    a & b \\
    c & d
\end{vmatrix}
```

$$
\begin{vmatrix}
    a & b \\
    c & d
\end{vmatrix}
$$

```tex
\begin{Bmatrix}
    a & b \\
    c & d
\end{Bmatrix}
```

$$
\begin{Bmatrix}
    a & b \\
    c & d
\end{Bmatrix}
$$

```tex
x = \begin{cases}
    a &\text{if } b \\
    c &\text{if } d
\end{cases}
```

$$
x = \begin{cases}
    a &\text{if } b \\
    c &\text{if } d
\end{cases}
$$

```tex
\begin{array}{cc}
    a & b \\
    c & d
\end{array}
```

$$
\begin{array}{cc}
    a & b \\
    c & d
\end{array}
$$

```tex
\begin{bmatrix}
    a & b \\
    c & d
\end{bmatrix}
```

$$
\begin{bmatrix}
    a & b \\
    c & d
\end{bmatrix}
$$

```tex
\def\arraystretch{1.5}
    \begin{array}{c:c:c}
    a & b & c \\ \hline
    d & e & f \\ \hdashline
    g & h & i
\end{array}
```

$$
\def\arraystretch{1.5}
    \begin{array}{c:c:c}
    a & b & c \\ \hline
    d & e & f \\
    \hdashline
    g & h & i
\end{array}
$$

```tex
\sum_{
\begin{subarray}{l}
    i \in \Lambda\\
    0 < j < n
\end{subarray}}
```

$$
\sum_{
\begin{subarray}{l}
    i \in \Lambda\\
    0 < j < n
\end{subarray}}
$$

```tex
\begin{equation}
\begin{split}
    a
    &= b + c \\
    &= e + f
\end{split}
\end{equation}
```

$$
\begin{equation}
\begin{split}
    a
    &= b + c \\
    &= e + f
\end{split}
\end{equation}
$$

```tex
\begin{gather}
    a = b \\
    e = b + c
\end{gather}
```

$$
\begin{gather}
    a = b \\
    e = b + c
\end{gather}
$$

```tex
\begin{align}
    a
    &= b + c \\
    d + d &= f
\end{align}
```

$$
\begin{align}
    a
    &= b + c \\
    d + d &= f
\end{align}
$$

```tex
\begin{alignat}{2}
    10&x + &3&y = 2 \\
    3&x + &13&y = 4
\end{alignat}
```

$$
\begin{alignat}{2}
    10&x + &3&y = 2 \\
    3&x + &13&y = 4
\end{alignat}
$$

## Letters and Unicode

### Greek Letters

|Syntax|Result|
|-|-|
|`\Delta`|$\Delta$|
|`\Theta`|$\Theta$|
|`\Sigma`|$\Sigma$|
|`\Phi`|$\Phi$|
|`\Omega`|$\Omega$|
|`\alpha`|$\alpha$|
|`\beta`|$\beta$|
|`\gamma`|$\gamma$|
|`\delta`|$\delta$|
|`\epsilon`|$\epsilon$|
|`\theta`|$\theta$|
|`\kappa`|$\kappa$|
|`\lambda`|$\lambda$|
|`\mu`|$\mu$|
|`\pi`|$\pi$|
|`\rho`|$\rho$|
|`\sigma`|$\sigma$|
|`\tau`|$\tau$|
|`\phi`|$\phi$|
|`\chi`|$\chi$|
|`\psi`|$\psi$|
|`\omega`|$\omega$|
|`\varepsilon`|$\varepsilon$|
|`\varphi`|$\varphi$|

### Other Letters

|Syntax|Result|
|-|-|
|`\nabla`|$\nabla$|
|`\ell`|$\ell$|
|`\hbar`|$\hbar$|
|`\R`|$\R$|
|`\partial`|$\partial$|

## Layout

### Annotation

|Syntax|Result|
|-|-|
|`\cancel{5}`|$\cancel{5}$|

```tex
\tag{hi} x + y^{2x}
```

$$
\tag{hi} x + y^{2x}
$$

### Vertical Layout

|Syntax|Result|
|-|-|
|`x_n`|$x_n$|
|`e^x`|$e^x$|
|`_u^o`|$_u^o$|
|`\sum_{\substack{0 < i < m \\ 0 < j < n}}`|$\sum_{\substack{0 < i < m \\ 0 < j < n}}$|

### Overlap and Spacing

```tex
\sum_{\mathclap{1 \le i \le j \le n}} x_{ij}
```

$$
\sum_{\mathclap{1 \le i \le j \le n}} x_{ij}
$$

#### Spacing

|Syntax|Produces|
|-|-|
|`\,`|3/18 em space|
|`\quad`|1 em space|
|`\qquad`|2 em space|

## Logic and Set Theory

|Syntax|Result|
|-|-|
|`\forall`|$\forall$|
|`\exists`|$\exists$|
|`\in`|$\in$|
|`\subset`|$\subset$|
|`\supset`|$\supset$|
|`\mid`|$\mid$|
|`\land`|$\land$|
|`\lor`|$\lor$|
|`\therefore`|$\therefore$|
|`\because`|$\because$|
|`\mapsto`|$\mapsto$|
|`\to`|$\to$|
|`\leftrightarrow`|$\leftrightarrow$|
|`\empty`|$\empty$|
|`\implies`|$\implies$|
|`\iff`|$\iff$|
|`\lnot`|$\lnot$|

## Macros

|Syntax|Result|
|-|-|
|`\def\foo{x^2} \foo + \foo`|$\def\foo{x^2} \foo + \foo$|
|`\gdef\foo#1{#1^2} \foo{y} + \foo{y}`|$\gdef\foo#1{#1^2} \foo{y} + \foo{y}$|

## Operators

### Big Operators

|Syntax|Result|
|-|-|
|`\sum`|$\sum$|
|`\int`|$\int$|
|`\iint`|$\iint$|
|`\iiint`|$\iiint$|
|`\oint`|$\oint$|
|`\prod`|$\prod$|

### Binary Operators

|Syntax|Result|
|-|-|
|`+`|$+$|
|`-`|$-$|
|`/`|$/$|
|`*`|$*$|
|`\bmod`|$\bmod$|
|`\cap`|$\cap$|
|`\cdot`|$\cdot$|
|`\cup`|$\cup$|
|`\div`|$\div$|
|`\land`|$\land$|
|`\lor`|$\lor$|
|`\pm`|$\pm$|
|`x \pmod a`|$x \pmod a$|
|`\times`|$\times$|

### Fractions and Binomials

|Syntax|Result|
|-|-|
|`{a \over b}`|${a \over b}$|

|Syntax|Result|
|-|-|
|`{n \choose k}`|${n \choose k}$|

### Math Operators

|Syntax|Result|
|-|-|
|`\arcsin`|$\arcsin$|
|`\arccos`|$\arccos$|
|`\arctan`|$\arctan$|
|`\cos`|$\cos$|
|`\operatorname{f}`|$\operatorname{f}$|
|`\argmax`|$\argmax$|
|`\argmin`|$\argmin$|
|`\det`|$\det$|
|`\cot`|$\cot$|
|`\csc`|$\csc$|
|`\lim`|$\lim$|
|`\max`|$\max$|
|`\exp`|$\exp$|
|`\lg`|$\lg$|
|`\ln`|$\ln$|
|`\log`|$\log$|
|`\min`|$\min$|
|`\sec`|$\sec$|
|`\sin`|$\sin$|
|`\tan`|$\tan$|

### \sqrt

|Syntax|Result|
|-|-|
|`\sqrt{x}`|$\sqrt{x}$|
|`\sqrt[3]{x}`|$\sqrt[3]{x}$|

## Relations

|Syntax|Result|
|-|-|
|`=`|$=$|
|`<`|$<$|
|`>`|$>$|
|`\approx`|$\approx$|
|`\equiv`|$\equiv$|
|`\ge`|$\ge$|
|`\gg`|$\gg$|
|`\in`|$\in$|
|`\le`|$\le$|
|`\ll`|$\ll$|
|`\perp`|$\perp$|
|`\propto`|$\propto$|
|`\sim`|$\sim$|
|`\sub`|$\sub$|
|`\supset`|$\supset$|

### Negated Relations

|Syntax|Result|
|-|-|
|`\ne`|$\ne$|

### Arrows

|Syntax|Result|
|-|-|
|`\gets`|$\gets$|
|`\to`|$\to$|

## Style, Color, Size, and Font

### Font

|Syntax|Result|
|-|-|
|`\text{Ab0}`|$\text{Ab0}$|
|`\Bbb{AB}`|$\Bbb{AB}$|
|`\bold{Ab0}`|$\bold{Ab0}$|
|`\texttt{Ab0}`|$\texttt{Ab0}$|

### Style

|Syntax|Result|
|-|-|
|`\displaystyle\sum_{i=1}^n`|$\displaystyle\sum_{i=1}^n$|
|`\lim\limits_x`|$\lim\limits_x$|

- `\text{...}` will accept neted `$...$` fragments and render them in math mode.

## Symbols and Punctuation

|Syntax|Result|
|-|-|
|`% comment`|$% comment$|
|`\_`|$\_$|
|`\S`|$\S$|
|`\text{\textcircled a}`|$\text{\textcircled a}$|
|`\textcircled a`|$\textcircled a$|
|`\dots`|$\dots$|
|`\cdots`|$\cdots$|
|`\ddots`|$\ddots$|
|`\vdots`|$\vdots$|
|`\blacksquare`|$\blacksquare$|
|`\infin`|$\infin$|
|`\angle`|$\angle$|
|`\degree`|$\degree$|
