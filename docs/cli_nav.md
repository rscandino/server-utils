# CLI Navigation Tools
Useful tools to navigate and interact with the filesystem through command line.

## Tree
The package `tree` provides a visual representation of a directory's contents in a tree-like format.
It's a powerful tool for quickly understanding the organization of files and subdirectories.

Running `tree` in a directory will display its contents recursively. Beyond this core function, tree offers a wide range of options (retrievable with `tree --help`) to customize its output, including:

* *File and Directory Listing*: The core function of tree is to list files and directories. It can be configured to show all files (`-a`), only directories (`-d`), or to follow symbolic links (`-l`). You can also specify the depth of the listing with -L and filter the output using include (`-P`) and exclude (`-I`) patterns. It can even respect .gitignore files (`--gitignore`).
* *File Information Display*: tree can show a wealth of metadata for each file. This includes permissions (`-p`), user and group ownership (`-u, -g`), file size (`in bytes -s or human-readable format -h`), modification or status change dates (`-D`), and inode numbers (`--inodes`).
* *Output Formatting and Sorting*: The output can be customized to be more visually appealing or useful. You can remove the indentation lines (`-i`), force colorization (`-C`), and append indicators like / or * to file names (`-F`). The output can also be sorted in various ways, including by name (`default`), modification time (`-t`), size (`--sort=size`), or unsorted (`-U`), with the option to reverse the sort order (`-r`).
* *Output to Other Formats*: Beyond the standard terminal output, tree has robust capabilities for generating output in machine-readable and web-friendly formats. It can produce XML (`-X`), JSON (`-J`), and HTML (`-H`) representations of the directory structure. This makes it a powerful tool for scripting, data analysis, and web documentation.
* *Input and Miscellaneous*: tree can also read paths from a file (`--fromfile`), and it provides options for specifying the character set (`--charset`), turning off the file count report (`--noreport`), and handling non-printable characters. It also supports creating terminal hyperlinks with the --hyperlink flag.

## Zoxide
[zoxide](https://github.com/ajeetdsouza/zoxide.git) is a smarter `cd` command. It remembers which directories you use most frequently, so you can "jump" to them in just a few keystrokes.

### Init
To fully work `zoxide` should be initialize on your `~/.bashrc`. Just add the following line:

```shell
eval "$(zoxide init bash)"
```

### Usage
:Important: Untill you enter into a directory it will not be memorized by `zoxide`.
It can be used in the same way of `cd`.
Here are the basic commands of `zoxide`:

```shell
z foo              # cd into highest ranked directory matching foo
z foo bar          # cd into highest ranked directory matching foo and bar
z foo /            # cd into a subdirectory starting with foo

z ~/foo            # z also works like a regular cd command
z foo/             # cd into relative path
z ..               # cd one level up
z -                # cd into previous directory

zi                 # toggle interactive selection (using fzf)
```

## Fzf
