---
title: Style Guide for Shell Scripts
pageid: lang-sh
keywords: $0 $1 $2 $a $aline $b $bash_source $debug_info $dest $destfile $file $result $some_variable $sourcefile $src $words &2 'case' 's +ee --another-option --finalize-and-write --option --sequence-step-addition --verbose -e -ee -eeo -gt -i -l -n -ne -v 0 0% 1 1% 2 3 4 80 a a-z above absolutely acceptable accessing accidentally add addition after again aim aline all allow allows almost always amount an and another anotherfunction any apart are args argument arguments array arrays as assist associative at avoid avoidance awk backslashes backticks bad basename bash bash-specific bash-strict-mode bash_source bashguide bashpitfalls basics be because becoming being below best better bin bit blank blob broken build but call calling calls camel camelcase can caps careful case cat cause cd change changes characters clean clever code coding collide colons com command commands comment comments compatibility complex conditions conflict consequences consistency constructs contents contexts conversely correctly cp crucial ctags dash debug debug_info declare default define dependencies depending describe descriptive destfile destination diagnostic did displayed do do-the-first-thing do-the-second-thing doc documentation documented does doesn't dog don't done double-quoted down each early echo either elementary eliminate enable enables encourage end ensure env environment equivalent error errors esac especially eval every example examples executable execute executed execution exist expansion expected expecting explain export expr extend extension external extract facilitate fail failing false fgrep fi file file's filename filenames filtering finally find first flawed folders for forbidden format from funcname function functionality functions g' general general-rules generates get github global globbing go goal goals goes good great greeting grep group handy happen happens has have hello help here hidden honored http https hyphens if ifs ignored immediately in include included increases indent inferring information informational initialize inner input inside inspiration instance instead intentionally internal interpreter into invoking is it its joining just keyword language language's languages largely leading learn least left let lets lib libraries library library's like likewise limit limits line lines list listed load loaded local long longer loop lowercase ls main make make-report makereport makes making mangles many markdown master match math may md meat meow merely messages mlafeldt mode more most multiple my my-program myprogram mywiki name named names namespaced naming necessary need nest net never newline non-empty non-zero nor normal normally not nothing numbers obtain of omit on one only open-ended operating optionally or order org other others our out output output-file outside override parameter parse pass pattern perhaps perl pipe piped pipefail pipes piping pitfalls portable portions posix possible practice practices practices#bash_tests prefer preferred prefix prefixes prepend prevent prevents printhello prints problem problems process processing program propagated public put quote read readability readable readonly reason redirection rely report requires reserved restricted result return returns reviewed right rules run run-a-very-complex-command run-command running runs safer same sample scan script scripts sed see semicolons separate seq set sh shall share shebang shell shellcheck shellcheck's should significantly silence simple situation slow so some some-file some_file some_variable somefile somefile-that-does-not-exist something source sourced sourcefile space spaces special speed split standard start state statement status stay stderr stdout stop stored strict string strings structure stuff subsequent subshell subshells subtle such support supported system system-wide take techniques template temporarily test tests-always-included text that the their them then there there's these they things this those though thought through ties tmp to together tomdoc tooling tools tr track tricks try two txt understandable unintended unintentional unless up uppercase usage use used using usr validate variable variables variables! variations verbose! version very want warning warnings way we we've web well what when where which while wick wick-infect wick-strict-mode wickstrictmode wickstrictrun will wish with within without won't woof wooledge words work workaround working workings would write writes writeup writing written www x y you your
---

These rules extend and override the [general rules][general-rules].

In addition to the normal goals, we want our shell scripts to be largely portable.  Depending on the situation, we may aim for compatibility with Bash 4, Bash 3 or a general POSIX system.


Tooling
-------

Use [ShellCheck](http://www.shellcheck.net/) to find problems.

[TomDoc.sh](https://github.com/tests-always-included/tomdoc.sh) lets you write TomDoc into shell scripts and extract it as markdown or text.  Very handy.


Basics
------

Shell scripts and libraries will start with a shebang, the `#!/usr/bin/env bash` bit for the first line of the file.  All shell scripts should use Bash.  To find bash, `env` will be used.  If speed is crucial, simple shell scripts can use `#!/bin/sh` or `#!/bin/dash`.

If you are only invoking `awk`, `sed`, `perl` or another language, you should use that language's interpreter instead of writing a shell script.  Conversely, you should prefer to stay within bash instead of calling out to perl or other languages as that increases the amount of dependencies that the script requires.

Bash-specific constructs shall be preferred, such as using `[[` instead of `[` or `test`.  There's a great writeup on [BashGuide/Practices](http://mywiki.wooledge.org/BashGuide/Practices#Bash_Tests).

Lines will be preferred to stop at 80 characters when possible, but longer lines are acceptable.  For instance, one may take a very long command and split it up so each argument is on a separate line for readability.  When you do split a line, indent the subsequent lines with 4 characters.

Don't nest commands together if possible.  This makes your code more readable.

    #!/usr/bin/env bash

    if [[ -n "$SOME_VARIABLE" ]]; then
        case "$SOME_VARIABLE" in
            dog)
                echo "woof woof"
                ;;

            cat)
                echo "meow"
                ;;

            *)
                echo "?"
                ;;
        esac

        echo "These commands have a blank line above to set them apart"
        echo "from the 'case' statement."
    fi

    # This command is not broken into multiple lines
    run-command --option=1 --another-option=2

    # This command is broken into multiple lines
    run-a-very-complex-command \
        --sequence-step-addition=do-the-first-thing \
        --sequence-step-addition=do-the-second-thing \
        --finalize-and-write=/tmp/output-file

    # This is a command that is piped through to others.
    # You do not need to use backslashes at the end.
    fgrep -v "OMIT" some_file.txt |
        sed 's/cat/dog/g' |
        tr a-z A-Z > output.txt

    echo "Done processing SOME_VARIABLE"


Variables and Functions
-----------------------

All things should use a descriptive name that would assist when inferring what the function does or what is stored in the variable.

Do not collide with system names, such as naming a function `test` or `cat`.  Prefer to use names with at least two words using `camelCase`.

Filenames will use hyphens and all lowercase, such as `make-report`.  Omit using `.sh` or `.bash` at the end of the filename.  Libraries and scripts will be executable as necessary so tools like `ctags` will scan the file for functions.

Function names will avoid hyphens in order to make them more portable.  Example:  `makeReport`.  If the script can be loaded as a library, the function names should be namespaced with the library's name and two colons; likewise, the main function should be named the same as the executable.

    #!/usr/bin/env bash
    # Sample library
    

    # Prints a greeting.
    #
    # Returns nothing.
    sample::printHello() {
        echo "Hello."
    }

   
    # This is the "main" of our program.
    sample() {
        # Just call the function
        sample::printHello
    }


    # Run if not sourced
    if [[ "$0" == "${BASH_SOURCE[0]}" ]]; then
        sample "$@"
    fi

Variable names will use camel case as well.  Use of uppercase names is restricted to system-wide variables and things you intentionally wish to export.  So, the function `makeReport` may use `sourceFile` and `destFile` as local variables.  Variables that are used that are not internal to the function will be in all caps, such as `DEBUG_INFO`.  When using an uppercase variable, prepend the variable to ensure it doesn't conflict with a reserved variable.

    # Generates a report.
    #
    # This is in the file "make-report".  This comment structure is
    # TomDoc.
    #
    # $1 - Source file.
    # $2 - Destination file.
    # DEBUG_INFO - If set to a non-empty string, writes debug information
    #              to stdout.
    #
    # Example
    #
    #   # Build a report from a template
    #   makeReport template.txt report.txt
    #
    # Returns nothing.
    makeReport() {
        local destFile sourceFile

        # ... Stuff happens here

        if [[ -n "$DEBUG_INFO" ]]; then
            echo "Making file: $sourceFile" >&2
        fi

        cp "$sourceFile" "$destFile"
    }


Coding Techniques and Problem Avoidance
---------------------------------------

Always code and enable a [strict mode](https://github.com/tests-always-included/wick/blob/master/doc/bash-strict-mode.md) or perhaps one like [Wick](https://github.com/tests-always-included/wick/blob/master/lib/wick-strict-mode).

Functions will list all of their variables as `local` to avoid unintentional consequences.  If accessing external variables, use `declare` to silence ShellCheck's warnings.

Initialize all variables to avoid unintended consequences and to assist with strict mode.

Do not rely on `IFS`.

If you have a list of things, track them as an array in your shell script and use the variable as an array.  This ties into the use of `IFS` as well as using `$@` instead of `$*` where possible.

Avoid the use of `eval` unless it is absolutely necessary.  There is almost always a better or safer way to do something.

Fail early.  This prevents work from being done accidentally in an error state.  When failing, return a non-zero status code.

Always validate the input from any source.

Using examples from the web are almost always flawed in some way.  Use them for inspiration and get the code reviewed to find hidden problems.

When possible, use the long version of arguments.  For example, instead of using `-v`, use `--verbose`.

Pipes into `while` will run the contents of the loop in a subshell, so changes to variables won't be propagated outside the loop.  Instead you may use process redirection.

    # Example while loop
    while read aLine; do
        echo "$aLine"
    done < <(fgrep -i line some-file.txt)


Consistency and Best Practices
------------------------------

Quote your variables!  Prevent problems when spaces are used in folders.  `cd $1` is bad, `cd "$1"` is the way to go.

Try to limit or eliminate subshells.  They slow down execution significantly.  You should use `{` and `}` to group commands unless you have a good reason to use `(` and `)`.

Use `$( command )` instead of backticks.

When making a command, have the script use a function and then optionally call the function.  This allows others to source the file into the environment and obtain the functionality.  There is an example of this pattern below, with `elementary`.

Your script should first set necessary global variables, then define functions, and finally have the "working code" that calls the functions.

Functions should use the more portable `funcName() {`, without the `function` keyword.

Output clean and understandable messages.  Normal messages are written to stdout.  Error and diagnostic information goes to stderr.  This enables output filtering and piping output to subsequent commands.

Learn to use `${0%/*}` instead of `basename "$0"`, `${1%*.}` to get a file's extension, and other parameter expansion techniques.

Do not add semicolons to the end of the lines.

Avoid joining commands.  `test && run-command` is not preferred.  `if test; then` (newline) `run-command` (newline) `fi` is the right way.  Be very careful when running commands in a strict mode and expecting them to fail correctly.  `set -e` is ignored in those contexts.  See the `elementary` example for a workaround.

Errors, warning and debug messages go to stderr.  Only expected output and informational messages are to be displayed on stdout in order to facilitate piping.

    #!/usr/bin/env bash

    # Load library functions
    . /usr/local/lib/wick-infect

    anotherFunction() {
        # This should fail
        ls -l somefile-that-does-not-exist

        # This should not happen but "set -e" is not honored inside conditions.
        echo "This should never execute."
    }

    elementary() {
        local result

        # Enable strict mode.  An equivalent is
        #   set -eEo pipefail
        wickStrictMode
        echo "These are the inner workings."
        echo "Args: $@"

        # This is a workaround because "set -e" is not honored in conditions,
        # such as when using if, while, !, ||, and others.  If not operating
        # in a Wick environment, an equivalent would be to temporarily set +eE
        # and run the command, and finally enable set -eE again.
        wickStrictRun result anotherFunction

        if [[ "$result" -ne 0 ]]; then
            echo "someFile does not exist"
        fi
    }

    # If sourced, this code does not run and the functions are merely loaded.
    # When executed as a command, this immediately runs the function.
    if [[ "$0" == "$BASH_SOURCE" ]] || ! [[ -n "$BASH_SOURCE" ]]; then
        elementary "$@"
    fi

Use double-quoted strings.


Comments and Documentation
--------------------------

Documentation will be done using TomDoc format (see [tomdoc.sh](https://github.com/mlafeldt/tomdoc.sh)).  That standard limits comments to 80 characters on a line.

Every function and public variable will be documented.

All complex portions and clever tricks will be documented to help explain the goal of the code.

Comments should not share a line with code.  Instead, put the comment above the code you wish to describe.

For usage documentation, prefix the lines with `#/` instead of `#` and include a space.  To avoid a line from becoming documentation because of TomDoc, either add a blank line after the comment or change the `#` into `#:`.

    #!/usr/bin/env bash
    #/ This is usage information.
    #/
    #/ my-program [--verbose]
    #/
    #/ --verbose - Be more verbose!

    # The meat of the program.
    #
    # $@ - All arguments
    #
    # Returns nothing.
    myProgram() {
        local WORDS

        #: Default to false.  (This comment would normally be included
        #: as TomDoc documentation but we've used special prefixes.)
        WORDS="these are words"

        if [[ $1 == "--verbose" ]]; then
            # Write the words.  (This comment did not need the prefix.)
            echo "$WORDS"
        fi
    }

    if [[ "$0" == "$BASH_SOURCE" ]] || ! [[ -n "$BASH_SOURCE" ]]; then
        myProgram "$@"
    fi


Forbidden
---------

Never parse `ls` output.  Its format can change, it mangles filenames.

Never use `echo "$file" | fgrep .txt` because it will match "sample.txt.sh".  Use globbing instead.

Never use `cat "$file" | grep "..."`.  Instead, most commands allow you to pass in the filename like `grep "..." "$file"`.  If that is not supported, pipe it in with `grep "..." < "$file"`.

Do not use a for loop to read a file, such as `for line in $(<$file); do`.  Instead use a while loop, like `while read line; do ... done < "$file"`.

Do not use `expr` to do simple math; use `((` and `))`.  Do not use `seq` to make a list of numbers; use `{x..y}`.  Avoid calling commands that Bash can do for you.

Do not use `let` nor `readonly`.  Only use `declare` for associative arrays.

There's many more things and subtle variations listed at [Bash Pitfalls](http://mywiki.wooledge.org/BashPitfalls).


Open-Ended
----------

You may use `[[ $a -gt $b ]]` or `(($a > $b))`.

Associative arrays may be used, though the goal for some commands is to work on Bash 3, which does not support them.

Using `cp "$src" "$dest"` may cause problems, especially when `$src` has leading hyphens.  Best practice would be to `cp -- "$src" "$dest"`, though that my not work for all commands.  This is left open-ended in order to encourage thought.


{% include links.html %}
