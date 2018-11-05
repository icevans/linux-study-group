# Unit 2: Redirection and Pipelines

The fundamental concepts here are the _standard input_, _standard output_, and _standard error_ streams; their default destinations; redirecting the default destinations, either to other files or to other commands. 

As you'll quickly see in chapter 6 of _The Linux Command Line_, pipelines are a very convenient method of chaining together commands. This chapter introduces us to many very powerful linux commands, including the seemingly oddly named 'grep'. These commands are more useful if we know about _wildcards_ a.k.a "file globbing."

* _The Linux Command Line_, chapter 4, section on "Wildcards" only
* _The Linux Command Line_, chapter 6
* [Kernighan on pipelines](https://www.youtube.com/watch?v=bKzonnwoR2I)
* [Kernighan on the origin of grep](https://www.youtube.com/watch?v=NTfOnGZUZDk)

Aside from their convenience is their low overhead: standard input, output, and error are _streams_, so what is being written to them does not need to be loaded into memory (or disk) all at once. Professor Kernighan alludes to this in the video on pipelines. These two wikipedia articles provide some more background, and the two simple Ruby programs I wrote demonstrate this (pipe `send_stream` to `read_stream` to watch this unfold -- detailed explanation coming soon). This pipeline depends on the fact that `Kernel#puts` writes to standard output, wile `Kernel#gets` reads from standard input.

https://en.wikipedia.org/wiki/Stream_(computing)
https://en.wikipedia.org/wiki/Standard_streams
http://ruby-doc.org/core-2.5.3/Kernel.html#method-i-gets
