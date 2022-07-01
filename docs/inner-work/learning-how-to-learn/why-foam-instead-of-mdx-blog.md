# Why Foam instead of MDX

Date: 2022-01-03

## Nicer UX

-   the UX is just nicer (tab will indent lists)
-   pasting images is super nice with foam
    -   the UX with MDX is manually copying
-   table of contents markdown creator/updater VSCode extension

### Lesser points

-   I can use (beautify) WYSIWYG markdown editors like [Typora](https://typora.io/) or [Zettlr](https://www.zettlr.com/)
    -   because I'm now just using regular Markdown (although I could get away with using MDX with those editors)
-   I haven't really used MDX that much anyway

### Problems with foam

I realized that I can just use GitHub

It doesn't have SEO or customizability but I don't really care about that right now.

-   My main concern is just getting stuff out of my head and into this system

I use Zettlr as my text editor because it has a nice left bar where I can navigate through all the files

I tried uploading to GitHub pages but encountered these problems

-   I have to create `index.md` pages that I'd have to manually
    -   I want to replicate the directory structure
-   2+ levels deep folders
    -   I like organization and grouping
    -   Foam's github pages
-   backlinks and forward links
-   automatic table of contents
    -   technically, this can be generated in markdown but the UI isn't the best
        -   I'd like to to be on the side rather than as a part of the content
-   no search

Alternatives I want to investigate

-   [neuron](https://github.com/srid/neuron-template)
    -   apparently it's in maintenance mode
    -   [emanote](https://github.com/srid/emanote) is the successor
    -   but it looks like it's not stable yet
-   mkdocs
-   GitBook: doesn't support 2+ levels deep
-   Bookstack and other hosted wikis
    -   we use this for work but you'd have to host a server and I'd rather not pay for a $5 a month DigitalOcean server
    -   it's really nice and is the basis of what I'd like
-
