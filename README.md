# argwrap.vim

argwrap.vim is an industrial strength argument wrapping and unwrapping extension for the [Vim](http://www.vim.org/) text
editor. It can be used for collapsing and expanding everything from function calls to array and dictionary definitions.
The online resources listed below can be accessed to download new versions of this extension and to access other related
information.

*   [Homepage](http://foosoft.net/projects/vim-argwrap/)
*   [GitHub](https://github.com/FooSoft/vim-argwrap/)
*   [Vim.org](http://www.vim.org/scripts/script.php?script_id=5062)

## Installation

1.  Clone or otherwise download the latest version of the *argwrap.vim* extension from its
    [GitHub](https://github.com/FooSoft/vim-argwrap) page (the script is also available for download through
    [vim.org](http://www.vim.org/scripts/script.php?script_id=5062)). If you are using
    [pathogen.vim](https://github.com/tpope/vim-pathogen) for plugin management (you should) you can clone the
    repository directly to your bundle directory:

    `git clone https://github.com/FooSoft/vim-argwrap ~/.vim/bundle/vim-argwrap`

2.  Create a keyboard binding for the `ArgWrap` command inside your `~/.vimrc` file. For example, to declare a normal
    mode mapping, add the following command:

    `nnoremap <silent> <leader>a :ArgWrap<CR>`

3.  You can customize the wrapping/unwrapping behavior of this extension by setting values for any of the following
    optional buffer and global variables in your `.vimrc` file:

    *   `g:argwrap_wrap_closing_brace` or `b:argwrap_wrap_closing_brace`

        Specifies if the closing brace should be wrapped to a new line. This setting is helpful when working with
        languages such as Google's [Go](https://golang.org/project/), which enforce coding style during compliation.

        Specifies if the closing brace should be wrapped to a new line. This setting is helpful for languages such as
        Google's [Go](https://golang.org/) which enforce this style during compliation.

        Brace wrapping enabled (default)

        ```
        Foo(
            wibble,
            wobble,
            wubble
        )
        ```

        Brace wrapping disabled (`let g:argwrap_wrap_closing_brace = 0`)

        ```
        Foo(
            wibble,
            wobble,
            wubble)
        ```

    *   `g:argwrap_padded_braces` or `b:argwrap_wrap_closing_brace`

        Specifies which brace types should be padded on the inside with spaces:

        `''`: do not add padding for any braces (empty string):

        ```
        [1, 2, 3]
        {1, 2, 3}
        ```

        `'['`: padding for square braces only (curly braces are not padded):

        ```
        [ 1, 2, 3 ]
        {1, 2, 3}
        ```

        Padding can be specified for multiple brace types as follows:

        ```
        let g:argwrap_padded_braces = '[{'
        ```

## Usage

1.  Position the cursor *inside* of the scope of the parenthesis, brackets or curly braces you wish to wrap/unwrap (not
    on top, before or after them).

2.  Execute the keyboard binding you defined above to *toggle* the wrapping and unwrapping of arguments.

## Examples

Below are some examples of common use cases demonstrating the capabilities of argwrap.vim. Note that the extension
functions identically regardless if it is being applied to a function call, list or dictionary definition.

Let's begin with a simple function invocation. When there are many arguments being passed to the function, we often wish
to wrap them to improve code readability. If you position your cursor anywhere between the parenthesis and execute the
`ArgWrap` command, the argument list will be wrapped to one per line.

```
Foo(wibble, wobble, wubble)

```

Becomes this:

```
Foo(
    wibble,
    wobble,
    wubble
)

```

List definitions work in a similar fashion:

```
foo = [bar, baz, qux, quux, corge]
```

Becomes this:

```
foo = [
    bar,
    baz,
    qux,
    quux,
    corge
]
```

Dictionaries also work the way you expected them to:

```
foo = {bar: 1, baz: 3, qux: 3, quux: 7}
```

Becomes this:

```
foo = {
    bar: 1,
    baz: 3,
    qux: 3,
    quux: 7
}
```

Finally, nested combinations of all the above are also supported:

```
Foo([wibble, wobble, wubble], spam, {bar: baz, qux: [1, 3, 3, 7]})
```

Becomes this:


```
Foo(
    [wibble, wobble, wubble],
    spam,
    {bar: baz, qux: [1, 3, 3, 7]}
)

```

You can continue argument expansion to:


```

Foo(
    [
        wibble,
        wobble,
        wubble
    ],
    spam,
    {
        bar: baz,
        qux: [
            1,
            3,
            3,
            7
        ]
    }
)

```

The argument wrapping and unwrapping operations demonstrated above are easily reversible and correctly preserve the
indentation of the surrounding code. This extension has been tested to work in scenarios of various complexity, but if
you discover a problem don't hesitate to report it.
