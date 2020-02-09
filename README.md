# Tufte Algorithms Book Template

[![pipeline status](https://gitlab.com/johnnychen94/tufte_algorithms_book/badges/master/pipeline.svg)](https://gitlab.com/johnnychen94/tufte_algorithms_book/commits/master)

This book template provides a starting point upon which authors may freely build to generate their own textbook entirely in LaTeX.
We used this setup for Algorithms for Optimization, and have continued to refine it for a new textbook on decision making under uncertainty.
The template allows for the direct compilation of a print-ready PDF, including support for figures, examples, and exercises.

We do all of our development in Ubuntu.


Install [Julia](https://julialang.org/downloads/platform.html).

Install LaTeX via texlive. We recommend [this repo](https://github.com/scottkosty/install-tl-ubuntu).

Clone the repository to a location of your choosing:
```
git clone https://github.com/sisl/tufte_algorithms_book.git
```

Initialize and update the submodules:
```
git submodule init
git submodule update
```

Compile the style:
```
cd style
sudo python setup.py install
cd ..
```

Compile the lexer:
```
cd lexer
sudo python setup.py install
cd ..
```

Install the required Julia packages. You can install it mannually, or you can use [`jlpkg`](https://github.com/fredrikekre/jlpkg) for a pip-like experience:
```julia
jlpkg --project=@. add $(cat REQUIRE | grep -v julia)
```

Install `pdf2svg`, which is used by PGFPlots (we assume Ubuntu - other operating systems may install pdf2svg differently):
```
sudo apt-get install pdf2svg
```

Install [pgfplots](https://ctan.org/pkg/pgfplots).

We require pythontex 0.17, which was just recently tagged. You will probably have to update your version on texlive on miktex. Alternatively, you can download the latest version of pythontex from https://github.com/gpoore/pythontex.

(Note that on arch-based systems, one should use tllocalmgr instead.)

## Test

Running `make test` pulls all the code and then runs all tests in `juliatest` blocks. See `runtests.jl` for details.

## Compilation

* `make compile` compiles the whole book
* `make compile CHAPTER = 'introduction chapter2\/introduction'` will comment out every `include` or `input` statement, except for `chapter/introduction` and `chapter/chapter2/introduction` where `chapter` can also be `appendix`. Requires `vim` to be installed.
* `make clean` removes all generated files except `book.pdf`

If you host your project under Gitlab, `.gitlab-ci.yml` is a CI/CD template to start with.

