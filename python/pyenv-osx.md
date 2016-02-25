Follow the steps in https://github.com/yyuu/pyenv#basic-github-checkout.

When installing a Python version to use, I had this problem:

pyenv install 3.4.4
Downloading Python-3.4.4.tgz...
-> https://www.python.org/ftp/python/3.4.4/Python-3.4.4.tgz
Installing Python-3.4.4...

BUILD FAILED (OS X 10.11.3 using python-build 20160202-10-ga6f1f48)

```
Inspect or clean up the working tree at /var/folders/yk/gj03l_qs0ngfrc1f8cwb13sr0000gn/T/python-build.20160225163921.19676
Results logged to /var/folders/yk/gj03l_qs0ngfrc1f8cwb13sr0000gn/T/python-build.20160225163921.19676.log

Last 10 log lines:
 File "/private/var/folders/yk/gj03l_qs0ngfrc1f8cwb13sr0000gn/T/python-build.20160225163921.19676/Python-3.4.4/Lib/ensurepip/__main__.py", line 4, in <module>
   ensurepip._main()
 File "/private/var/folders/yk/gj03l_qs0ngfrc1f8cwb13sr0000gn/T/python-build.20160225163921.19676/Python-3.4.4/Lib/ensurepip/__init__.py", line 209, in _main
   default_pip=args.default_pip,
 File "/private/var/folders/yk/gj03l_qs0ngfrc1f8cwb13sr0000gn/T/python-build.20160225163921.19676/Python-3.4.4/Lib/ensurepip/__init__.py", line 116, in bootstrap
   _run_pip(args + [p[0] for p in _PROJECTS], additional_paths)
 File "/private/var/folders/yk/gj03l_qs0ngfrc1f8cwb13sr0000gn/T/python-build.20160225163921.19676/Python-3.4.4/Lib/ensurepip/__init__.py", line 40, in _run_pip
   import pip
zipimport.ZipImportError: can't decompress data; zlib not available
make: *** [install] Error 1
```

I tried `brew install homebrew/dupes/zlib` but that didn't help, but a tip from https://github.com/yyuu/pyenv/issues/454 did.

```
$ xcode-select --install
xcode-select: note: install requested for command line developer tools

$ pyenv install 3.4.4
Downloading Python-3.4.4.tgz...
-> https://www.python.org/ftp/python/3.4.4/Python-3.4.4.tgz
Installing Python-3.4.4...
Installed Python-3.4.4 to /Users/scott/.pyenv/versions/3.4.4
```

Don't forget to `pyenv rehash`
