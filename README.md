# binstall

**binstall** is a simple tool installer ("bin installer") designed for situations where you just need a set of tools available on a system without root access. It's a self-contained ruby script which only depends on the basic tools available on most unixlike systems (curl, tar, chmod, ...).

## Usage

Copy the script to the target server and run it. Binaries are installed to `$HOME/opt` so you may need to add that to `$PATH`.

## Default toolset

- direnv
- dua
- fd
- fselect
- fzf
- jc
- jless
- ripgrep
- sd
- skim
- tokei
- watchexec

## Contributions

Open an [issue](https://github.com/crdx/binstall/issues) or send a [pull request](https://github.com/crdx/binstall/pulls).

## Licence

[GPLv3](LICENCE).
