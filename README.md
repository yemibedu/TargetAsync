
# Target Concurrency

run FAKE Targets using concurrency to speed up execution.

This library does route finding and path optimization to enable the grouping of targets that can run in parallel.

`
#r "./lib/Bedu.TargetConcurrency.dll"
`
open Bedu
`

`
open TargetConcurrency
`

`
Target "_A" DoNothing ; Target "_B" DoNothing ; Target "_C" DoNothing
`

`
Target "_D" DoNothing ; Target "_E" DoNothing ; Target "_F" DoNothing
`

`
Target "_G" DoNothing ; Target "_H" DoNothing
`

`
"_A" ==> "_B" ; "_A" ==> "_C"
`

`
"_B" ==> "_D" ; "_C" ==> "_D"
`

`
"_D" ==> "_E" ; "_D" ?=> "_G" ; "_F" ?=> "_G"
`

`
"_E" ==> "_H" ; "_G" ==> "_H"
`

`
runTargetConcurrent "_H"
`

A

/\

B , C

\/

D | F

/\? /?

E , G

\/

H

# Known Issues
1) Since this is external to the actual F# Fake Library, it can not directly access *changeExitCodeIfErrorOccured()*

# See Also
1) [FAKE - F# Make - A DSL for build tasks](http://fsharp.github.io/FAKE/)

2) [Parallel Target JIT?](https://github.com/fsharp/FAKE/issues/1395) for the problem this is trying to solve.
