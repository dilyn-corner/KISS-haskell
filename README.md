|/
|\ISS                                                           https://k1ss.org
________________________________________________________________________________


KISS-haskell - A KISS repository for Haskell projects
________________________________________________________________________________

# KISS-haskell

I needed to batch convert .docx to .pdf. The easiest way I know of is via pandoc. 

pandoc-bin is in Community. 

For *good* reason. 

Luckily, [somebody](https://github.com/redneb/ghc-alt-libc/) went through the hard work of compiling GHC on musl from a glibc distro already. So we use his work to bootstrap a proper GHC build. From there, we can get cabal for all of our packages if we want to. Alternatively, we can package them and abuse cabal. Because why do languages need their own package manager? 


If you do not have a working GHC, install `ghc-bootstrap` first (you'll have no choice; `ghc` will fail to build). Then build `ghc`, and then uninstall the bootstrap before installing the full thing. That is, in order:
1. `kiss b ghc-bootstrap`
2. `kiss i ghc-bootstrap`
3. `kiss b ghc`
4. `kiss r ghc-bootsrap`
5. `kiss i ghc`

Note: if you get an error about a missing `libtinfo.so.6`, it's because we don't make one with KISS' `ncurses`. It is still required for god-knows-why; merely do the following:
```ln -s /usr/lib/libncursesw.so.6 /usr/lib/libtinfo.so.6```



The first two steps will take almost no time. Because we use an llvm-perf build of GHC, it takes far longer. On my 2014 Macbook Pro (2.6Ghz i5, 8GB DDR3), upwards of 4 hours. Have fun!
