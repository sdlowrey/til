# Anatomy of a Haskell module

Starting from the top, a view of a production Haskell module that facilitates an advanced command line UI.  See Hoogle for details.

## Pragma

Non-grammar hints and directives that modify language, compiler, interpreter, or assembler environment or behavior.

Pragmas are common to most languages and they are often equivalent to command options.

The pragmas in this example enable specific static or dynamic language options.

```
{-# LANGUAGE DeriveGeneric       #-}
{-# LANGUAGE FlexibleContexts    #-}
{-# LANGUAGE LambdaCase          #-}
{-# LANGUAGE MultiWayIf          #-}
{-# LANGUAGE NoImplicitPrelude   #-}
{-# LANGUAGE OverloadedStrings   #-}
{-# LANGUAGE RecordWildCards     #-}
{-# LANGUAGE ScopedTypeVariables #-}
{-# LANGUAGE TemplateHaskell     #-}
```

## Module

A singular definition of the contents of an exported module. A module defines a flat namespace.  Modules are not related to the underlying file system structure.

A module declaration consists of a capitalized name and and optional list of exports in parentheses.  If no exports are defined, then all top-level bindings are exported.

All exported entities must be declared or imported within the module.

Modules and their names can be imported by other modules.

The `where` keyword begins the definition of the module (also used with instance and class definitions, `let` expressions, etc).


```
module Acme.Client
  ( module Acme.Client.Types
  , status
  , run
  , RunOptions (..)
  ) where
```

The first thing exported in this example is `Acme.Client.Types`, which itself is a module imported by this one.

`RunOptions` is a class or type. The `(..)` means that all methods/constructors are exported.

## import

Imports bring other modules or module entities into a module's namespace. These entities are top-level declarations with global scope.  Imported names can be aliased with `as`.

```
import           Control.Concurrent                 (threadDelay)
import qualified Data.Aeson                         as Json
import           Data.Aeson.Encode.Pretty
import           Acme.Client.Types                 hiding (fid, state)
```

In this example:

`Control.Concurrent` is a module. (Is `Concurrent` a module from the `Control` package? Not sure, doesn't matter yet.)  The function `threadDelay` is being imported.

`Data.Aeson` is a module. To avoid name collisions with other modules, the `qualified` keyword tells the compiler not to bring the module name into scope. Calls to `Data.Aeson` functions will be prefixed with `Json.` in the scope of the importing module.

`Acme.Client.Types` is imported (and exported, as noted above) except for the `fid` and `state` entities, which are hidden. Hiding prevents unwanted shadowing by unused entities.

## Function definition

Functions have a type signature and a definition.

```
exitFailure :: Client a
exitFailure = liftIO Exit.exitFailure
```

The first line is a type definition and the second is the function definition.

The type identifier is `exitFailure` and the type is `Client` (which accepts an argument `a`).  For this example, it is informative to look up the definition of `Client`, which (I think) is a type synonym that defines a new identifier for a group of types.  

```
type Client = ReaderT ClientState Expr
```

Anyway, the function name is `exitFailure` and it accepts no arguments. It "lifts" a computation from the `IO` monad `Exit.exitFailure`. (not shown: `Exit` is an alias for `System.Exit`, which is an `IO` monad.)
