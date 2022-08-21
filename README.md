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

## Extending

This script is designed for developers, so extending it involves modifying the code.

Each tool is defined by a class inheriting from `Installer` mentioned in `Installer::INSTALLABLES`.

As an example let's look at the definition for `jless`.

```ruby
class Jless < Installer
    NAME = 'jless'
    REPO = 'PaulJuliusMartinez/jless'

    def install!
        basename = "jless-v#{latest_version}-x86_64-unknown-linux-gnu.zip"
        url = "https://github.com/#{REPO}/releases/download/v#{latest_version}/#{basename}"
        extract_zip!(url)
        chmod!
    end
end
```

Each installer must contain:

- A `NAME` constant for the binary filename.
- A`REPO` constant for the path of the repository on GitHub.
- An `install!` method whose responsibility it is to install the tool. This method is only called if the tool is missing or out-of-date.

Inside the `install!` method various helpers are accessible:

#### `extract_tar_xz!(url, basename)`

Download a `tar.xz` file and extract the binary out of the archive. `basename` should be provided if the archive is laid out such that the files are inside a top-level root folder.

#### `extract_gz!(url)`

Download a `gz` file and extract it.

#### `extract_zip!(url)`

Download a `zip` file and extract it.

#### `extract_tar_gz!(url, basename)`

Download a `tar.gz` file and extract the binary out of the archive. `basename` should be provided if the archive is laid out such that the files are inside a top-level root folder.

#### `download!(url)`

Download a file.

#### `chmod!`

Ensure that the binary has executable (`+x`) permissions.

#### `latest_version`

Fetch the version of the latest release from GitHub.

## Contributions

Open an [issue](https://github.com/crdx/binstall/issues) or send a [pull request](https://github.com/crdx/binstall/pulls).

## Licence

[GPLv3](LICENCE).
