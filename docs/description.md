# Description

This document provides a high level description of the project, in terms of the OS, the standard tools, and the implementing language.

## Language

The language the OS is implemented in will be a functional language supporting the following features:

* Algebraic Data Types
* Parametric Types
* Higher-kinded quantification
* Monadic IO (through a separate judgment, rather than through a generic monad interface)

## Tools

The tools that are built on top of the OS will all be typed with a rich type system that allows for degradation of the types into less informative ones. The types should be the same as the language's types. Degradation should be permitted to simpler things like non-recursive tuple types over basic types, and then down to just strings.

Recovery of structure should happen by transforming the types from static information into runtime information. E.g. if statically we know that `M : A` then we should be able to convert `M` to `bytes M`, which is just `M` but seen as some bytes, and convert `A` to `syntax A`, which is just some runtime syntactic representation of `A`, and then at runtime do `parseAs (bytes M) (syntax A)` and the result should be something structurally equal to `M` (perhaps with tyope information annotated?). Probably `syntax A` could be also just `bytes A`.

All tools will need to implement not just things like `stdin` and `stdout` but also a type signature, which can then be used by systems for composing tools.

### GUI Tools

We also want to make sure that if we make GUI tools, that they retain the compositionality of the non-GUI tools. Instead of having an application-oriented framework, we want to be sure to have a data-oriented and function-oriented framework for GUIs. What this means is not entirely clear, however.
