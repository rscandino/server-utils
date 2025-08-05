# CLI Navigation Tools
Useful tools to navigate and interact with the filesystem through command line.

## Tree
The package `tree` provides a visual representation of a directory's contents in a tree-like format.
It's a powerful tool for quickly understanding the organization of files and subdirectories.

Running `tree` in a directory will display its contents recursively. Beyond this core function, tree offers a wide range of options (retrievable with `tree --help`) to customize its output, including:

1. **Listing & Filtering**:

    * *Control what is shown*: Display all files (-a), only directories (-d), or respect .gitignore files (--gitignore).
    * *Filter by patterns*: Include (-P) or exclude (-I) files and directories that match a specific pattern.
    * *Limit depth*: Restrict the output to a specific number of directory levels (-L).

2. **Information Display**: Show permissions (-p), owner/group (-u, -g), size (-s, -h), and modification dates (-D).

3. **Sorting & Ordering**:

    * *Sort options*: Order the output by name (default), modification time (-t), size (--sort=size), or other criteria.
    * *Customization*: Reverse the sort order (-r) or list directories before files (--dirsfirst).

4. **Output Formats**:

    * *Standard output*: Prints a visual tree to the console.
    * *Machine-readable formats*: Export the tree as JSON (-J), XML (-X), or HTML (-H).
    * *File output*: Redirect the output to a file instead of the terminal (-o).


## Zoxide
[zoxide](https://github.com/ajeetdsouza/zoxide.git) is a smarter `cd` command. It remembers which directories you use most frequently, so you can "jump" to them in just a few keystrokes.

### Init
To fully work `zoxide` should be initialized in your `~/.bashrc`. Just add the following line:

```shell
eval "$(zoxide init bash)"
```

### Usage
:bangbang: Untill you enter into a directory it will not be memorized by `zoxide`.
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
