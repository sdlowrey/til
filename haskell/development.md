# Haskell Development on Mac

_Refer to the install-haskell-osx.md to get set up._

# Build

## stack
_Learned: it's better to use stack than cabal. Avoids dependency hell by using package snapshots._

http://docs.haskellstack.org/en/stable/README/

1. `cd project-dir`
2. `stack build`
3. `export PATH=.stack-work/install/x86_64-osx/lts-5.0/7.10.3/bin:$PATH`
  4. I prepended my path so that the project binaries are used instead of the homebrew version. Be aware of that if you want to fall back.


https://wiki.haskell.org/How_to_write_a_Haskell_program#Build_your_project

## cabal

You can use cabal, but build errors can be the result of dependency conflicts. Stack is faster and more reliable.

1. Change to a source directory where there is a Setup.hs.
2. `cabal sandbox init`
3. `cabal install -j`
