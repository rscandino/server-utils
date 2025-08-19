# :rocket: File System Navigation Tools
Useful tools to navigate and interact with the filesystem through command line.

1. [tree](#deciduous_tree-tree)
2. [zoxide](#rabbit-zoxide)
3. [ripgrep](#crystal_ball-ripgrep)
4. [fzf](#mag_right-fzf)

---

## :deciduous_tree: Tree
The package `tree` provides a visual representation of a directory's contents in a tree-like format.
It's a powerful tool for quickly understanding the organization of files and subdirectories.

Running `tree` in a directory will display its contents recursively. Beyond this core function, `tree` offers a wide range of options (retrievable with `tree --help`) to customize its output, including:

1. **Listing & Filtering**:

    * *Control what is shown*: Display all files (`-a`), only directories (`-d`), or respect .gitignore files (`--gitignore`).
    * *Filter by patterns*: Include (`-P`) or exclude (`-I`) files and directories that match a specific pattern.
    * *Limit depth*: Restrict the output to a specific number of directory levels (`-L`).

2. **Information Display**: Show permissions (`-p`), owner/group (`-u, -g`), size (`-s, -h`), and modification dates (`-D`).

3. **Sorting & Ordering**: Order and sort the output by name, modification time (`-t`), size (`--sort=size`), or other criteria.

4. **Output Formats**: Export the tree as JSON (`-J`), XML (`-X`), or HTML (`-H`).

```shell
# Some examples
tree                        # displays files and dirs (recursively) of current directory
tree -d                     # displays dirs only (recursively) of current directory
tree Documents/             # displays files and dirs of directory Documents
tree -h                     # displays file size (human readable) of current directory
```


## :rabbit: Zoxide
[zoxide](https://github.com/ajeetdsouza/zoxide.git) is a smarter `cd` command. It remembers which directories you use most frequently, so you can "jump" to them in just a few keystrokes.

### Init
To fully work `zoxide` should be initialized in your `~/.bashrc`. Just add the following line:

```shell
 # Set up zoxide key bindings
which zoxide &> /dev/null;
if [ $? -eq 0 ]; then
  eval "$(zoxide init bash)"
fi
```

>[!Note]
> You can assign zoxide keybind to another command (like `cd`) by adding the line `--cmd <your new command>` without specifying aliases.
> e.g. `eval "$(zoxide init bash --cmd cd)"`, this is activate zoxide using the command cd instead of the default z.


Remeber to `source ~/.bashrc` after.

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

## :crystal_ball: Ripgrep
[ripgrep](https://github.com/BurntSushi/ripgrep.git) is a line-oriented search tool that recursively searches the current directory for a regex pattern.
By default, ripgrep will respect gitignore rules and automatically skip hidden files/directories and binary files.

It is a faster and more powerfull version of `grep`. Just type `rg` followed by the pattern you are looking for. Several flags are availabe just look at the manual or the [repo](https://github.com/BurntSushi/ripgrep.git).

```shell
# Some examples
rg lol                          # looks for pattern 'lol' in all the files present in current dir
rg lol README.md                # looks for pattern 'lol' in file README.md
rg '[A-Za-z]{30}' README.md     # looks for regex '[A-Za-z]{30}' in file README.md

```
## :mag_right: Fzf
General-purpose command-line fuzzy finder. It's an interactive **filter program** for any kind of list; files, command history, processes, hostnames, bookmarks, git commits, etc.
It implements a "fuzzy" matching algorithm, so you can quickly type in patterns with omitted characters and still get the results you want.

The basic usage of `fzf` is indeed to be added at the and of a command generating a list/search/selection. It matches nicely with other tools such as `find`, `ripgrep`, `fd-find`, but it can be also be paired with text editors etc.:

```shell
rg <pattern> | fzf          # fuzzy find selection of 'ripgrep' serach of <pattern>
find * -type f | fzf        # fuzzy find selection of files of the 'find' tool
ls | fzf                    # fuzzy find 'ls' results
vim $(fzf)                  # Open selection of fzf (as a bash variable) into 'vim'
```

It can also be matched with tmux and its configuration and many other tools, check directly the [repo](https://github.com/junegunn/fzf.git).

### Configuration
Add the following line to your `~/.bashrc`. This enables cool stuff like fuzzy find your history with `Ctrl+r`.
eval "$(fzf --bash)"

### Fuzzy completition for bash (Simplest usage!)
`fzf` is be included by default for **autocomplete** using the command `**` followd by pressing `<TAB>` key:

```shell
vim **<TAB>                     # fuzzy autocomplete
vim Documents/**<TAB>           # fuzzy autocomplete inside Documents dir
cd **<TAB>                      # Another example of fuzzy autocomplete
```

### Customize commands
`fzf` has different flags that can be used to customize its usage, for example:

```shell
ls | fzf --preview "cat {}"                              # display preview of the selection using 'cat'
ls | fzf --preview "batcat -n --color=always {}"         # display preview of the selection using 'bat' and colors
```

All customizations can be made permanent by setting export variables into your `~/.bashrc` file. Check the [repo](https://github.com/junegunn/fzf.git) for more.
