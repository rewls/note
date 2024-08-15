# GNU 'sed'

> Version 4.8
>
> `info sed`

## 2 Running sed

### 2.1 Overview

- Normally 'sed' is invoked like this:

	```sh
	sed SCRIPT INPUTFILE...
	```

- If you do not specify INPUTFILE, or if INPUTFILE is '-', 'sed' filters the contents of the standard input.

- 'sed' writes output to standard output.

- By default 'sed' prints all processed input.

- Use '-n' to suppress output, and the 'p' comand to print specific lines.

- Without '-e' or '-f' options, 'sed' uses the first non-option parameter as the SCRIPT, and the following non-option parameters as input files.

### 2.2 Command-Line Options

- The full format for invoking 'sed' is

	```sh
	sed OPTIONS... [SCRIPT] [INPUTFILE...]
	```

## 3 'sed' scripts

- A 'sed' program consists of one or more 'sed' commands.

- 'sed' commands follow this syntax:

	```sh
	[addr]X[options]
	```

- X is a single-letter 'sed' command.

- '[addr]' is an optional line address.

- If '[addr]' is specified, the command X will be executed only on the matched lines.

- '[addr]' can be a single line number, a regular expression, or a range of lines.

- Additional '[options]' are used for some 'sed' commands.

- Commands within a SCRIPT or SCRIPT-FILE can be separated by semicolons or newlines.

### 3.2 'sed' commands summary

- The following commands are supported in GNU 'sed'.

- (Mnemonics) are shown in parentheses.

- 'n' (next)

	- replace the pattern space with the next line of input.

	- If there is no more input then 'sed' exits without processing any more commands.

- 'p'

	- Print the pattern space.

- 'd'

    - Delete the pattern space; immediately start next cycle.

## 4. Addresses: selecting lines

### 4.1 Addresses overview

- Addresses determine on which line(s) the 'sed' command will be executed.

- If no address is specified, the command is performed on all lines.

- Addresses can contain regular expressions to match lines based on content instead of line numbers.

- An address range is specified with two addresses separated by a comma(',').

- Addresses can be numeric, regular expressions, or a mix of both.

### 4.2 Selecting lines by numbers

- Addresses in a 'sed' script can be in any of the following forms:

    - 'NUMBER'

        - Specifyign a line number will match only that line in the input.

### 4.3 Selecting lines by text matching

- GNU 'sed' supports the following regulare expression addresses.

    - '/REGEXP/'

        - This will select any line which matches the regular expression REGEXP.
