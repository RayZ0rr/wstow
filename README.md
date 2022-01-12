# wstow :- A stow wrapper

## What ?
wstow is a wrapper around GNU stow that makes it easier to make symlinks from multiple sources to multiple targets easily.

## Why ?
[GNU stow](https://www.gnu.org/software/stow/ "GNU stow") is a symlink maker and manager that makes multiple symlinks easier. However, it still lacks some capabilites that makes it difficult to symlink multiple distinct package groups. Take a look at following example :  
[*Here assumed current working directory is home ( `~` or `/home/<username>`*) and dotfiles is at `~/path/to/dotfiles` ]  

---
- **To make symlinks to multiple folders under your config directory, eg : `vifm`, `nvim`, `bat`, `zsh` with stow**
1. got to .config directory ( `cd ~/.config` )
2. Create vifm directory ( `mkdir vifm` )
3. Go to vifm directory ( `cd vifm` )
4. Use stow to symlink ( `stow -v -t ./ -d ../path/to/dotfiles/.config -S vifm` )
5. go back to .config directory ( `cd ..` )
6. Repeat from step 2 replacing '`vifm`' with any other package name ( like `nvim`, `zsh` , `alacritty`)  
---
- **To make symlinks to multiple folders under your config directory, eg : `vifm`, `nvim`, `bat`, `zsh` with wstow**
1. `wstow file ../path/to/dotfiles/.config ./ vifm alacritty zsh bat`
( The syntax is like this :-
`wstow mode SOURCE_DIR TARGET_PARENT_DIR PACKAGE_NAMES` )  
---

## Dependencies
1. [Stow](https://www.gnu.org/software/stow/)
2. `find` for `ignore` and `fignore` modes

# Install
Just copy the script to anywhere in your _`PATH`_ ( `echo $PATH` ). Make sure the script is executable ( `chmod +x wstow` )

# Usage

The syntax for wstow is :-
`wstow mode SOURCE_DIR TARGET_PARENT_DIR PACKAGE_NAMES`
1. **mode**
- `dry` :- Do not make any changes. Just do dry-run or simulate what the changes will be made with `file` mode  

- `file` :- For all the `PACKAGE1`, `PACKAGE2`,... from `PACKAGE_NAMES` make symlinks for all files from `SOURCE_DIR/PACKAGE1`,`SOURCE_DIR/PACKAGE2`,... inside the folder `TARGET_PARENT_DIR/PACKAGE1`, `TARGET_PARENT_DIR/PACKAGE2`,.. till all the `PACKAGE_NAMES`. Recurse into subdirectories in `PACKAGE1`, `PACKAGE2`,... and create symlinks. The subdirectories will also be created (stow `--no-folding` feature).
- `folder` :- For all the `PACKAGE1`, `PACKAGE2`,... from `PACKAGE_NAMES` make symlinks for files and folder from `SOURCE_DIR/PACKAGE1`,`SOURCE_DIR/PACKAGE2`,... inside the folder `TARGET_PARENT_DIR/PACKAGE1`, `TARGET_PARENT_DIR/PACKAGE2`,.. till all the `PACKAGE_NAMES`. Symlinks for first level subdirectories are created without recursing like `file` mode.  
(**_Note :exclamation: :- Files/folders deleted inside a symlinked folder will delete original source. To remove a symlinked folder, delete the symlinked folder. Deleting the contents inside will delete from original source_**.)
- `ignore` :- Similar to `file` mode except all packages from `SOURCE_DIR` will be used except for those provided as `PACKAGE_NAMES`.
- `fignore` :- Similar to `folder` mode except all packages from `SOURCE_DIR` will be used except for those provided as `PACKAGE_NAMES`.
- `restow` :- Similar to `folder` mode except re-stow or repair symlinks
- `delete` :- Similar to `folder` mode except delete symlinks. ( When used to remove symlinks from `file` mode, empty subdirectories would remain.)
###End
