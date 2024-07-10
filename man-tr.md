# `man tr`

## Name

- tr - translate or delete characters

## Synopsis

```sh
tr [OPTION]... STRING1 [STRING2]
```

## Description

- Translate, squeeze, and/or delete characters from standard input, writing to standard output.

- STRING1 and STRING2 specify arrays of characters ARRAY1 and ARRAY2 that control the action.

- ARRAYS are specified as strings of characters.

- Mostrepresent themselves.

- Interpreted sequences are:

    - CHAR1-CHAR2: all chracters from CHAR1 to CHAR2 in ascending order

    - [:alnum:]: all letters and digits

    - [:alpha:]: all letters

    - [:digit:]: all digits
