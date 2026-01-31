
+++
pubdate = Date("2026-01-30")
title = "How reproducible is an renv environment, really?"
showall = true
category = "programming"
tags = ["programming", "reproducibility"]
+++

Modern programming languages provide environment managers to support reproducibility.


There is a myriad of things that can affect the reproducibility of the results of a code (e.g., system libraries), but changes in packages and languages across versions are a big source of variation in behavior. Therefore, a system is needed so that, given a version of the programming environment and an specification of the packages and their versions, code will continue to work as long as the specified environment is present. An environment manager helps keep track of these elements. Furthermore, most modern environment managers help recover that state by installing the specified versions from available sources. This helps sharing code with collaborators and reusing code from ancient projects, for example.


I recently tried reproducing an environment for the R language. The R version used originally was 4.0.3, released in 2020. The environment manager is [renv](https://rstudio.github.io/renv/) and my OS is macOS Tahoe 26.2. (The OS where I first saw the issue is Linux with CentOS 8, but I am reproducing the problem in my Mac). Old software, but I think this is what an environment manager should be good at. 


Here is a minimal `renv.lock` that reproduces the issue with only one package. `renv.lock` [is the file used in renv to specify the versions of packages and of the R language used in a project](https://rstudio.github.io/renv/articles/renv.html#getting-started). The example below is not a very difficult situation because I am not requesting conflicting package versions, just one package (which should bring its own set of dependencies).


```json
{
  "R": {
    "Version": "4.0.3",
    "Repositories": [
      {
        "Name": "CRAN",
        "URL": "https://cran.r-project.org"
      }
    ]
  },
  "Packages": {
    "GGally": {
      "Package": "GGally",
      "Version": "2.1.0",
      "Source": "Repository",
      "Repository": "CRAN"
    }
  }
}
```

I put this on a working folder. Fired up my R 4.0.3 console, run `renv::activate()` to get some infrastructure set up. Then, I try to "restore" the environment by installing the specified versions.


```bash
Rscript -e "options(pkgType = 'source'); renv::restore()"
```


In here, I use the option `pkgType = 'source'` to tell renv to install the packages from source. This is to reproduce the way R installs packages in Linux(*). The result of that line is a failure to install the package due to a dependency (`forcats`) not being available. Bad news.


```
# Bootstrapping renv 1.1.7 ---------------------------------------------------
- Downloading renv ... OK
- Installing renv  ... OK

- None of the packages recorded in the lockfile are currently installed.
- Use `renv::restore()` to restore the project library.
The following package(s) will be updated:

# CRAN -----------------------------------------------------------------------
- GGally   [* -> 2.1.0]

Error: package 'forcats' is not available
Traceback (most recent calls last):
```


This problem seems to come from the fact that in the main repository for R packages (CRAN) [packages can be removed](https://cran.r-project.org/web/packages/policies.html) and [archived](https://cran.r-project.org/src/contrib/Archive/) (let's also link this in here, why not? [Is CRAN holding R back?](https://arilamstein.com/blog/2025/02/12/is-cran-holding-r-back/)). On the other hand, renv environment manager [is only equipped to search for package dependencies in the main index of the CRAN repository, and not in the archives](https://github.com/rstudio/renv/issues/1735). If we take a look at the current index (visited on Jan 31 2026), we can see that the available version for `forcats` is not available for R 4.0.3. Game over.

```
forcats: Tools for Working with Categorical Variables (Factors)

Helpers for reordering factor levels (including moving specified levels to front, ordering by first appearance, reversing, and randomly shuffling), and tools for modifying factor levels (including collapsing rare levels into other, 'anonymising', and manually 'recoding').
Version: 	1.0.1
Depends: 	R (≥ 4.1)
Imports: 	cli (≥ 3.4.0), glue, lifecycle, magrittr, rlang (≥ 1.0.0), tibble
Suggests: 	covr, dplyr, ggplot2, knitr, readr, rmarkdown, testthat (≥ 3.0.0), withr
Published: 	2025-09-25
DOI: 	10.32614/CRAN.package.forcats
Author: 	Hadley Wickham [aut, cre], Posit Software, PBC ROR ID [cph, fnd]
Maintainer: 	Hadley Wickham <hadley at posit.co>
BugReports: 	https://github.com/tidyverse/forcats/issues
License: 	MIT + file LICENSE
URL: 	https://forcats.tidyverse.org/, https://github.com/tidyverse/forcats
NeedsCompilation: 	no
Materials: 	README, NEWS
CRAN checks: 	forcats results
```


The difficulty in reproducing my environment is a mixture between the environment manager itself and the way (CRAN) the most used package repository works. In essence, the renv/CRAN combo seem to ensure reproducibility of an environment only in the short term, when you can trust that all the packages will still be available for your R version in the main index of the CRAN repository.


There are workarounds (setting as the source for packages, a specific historical snapshot of a repository where all your packages were available, or iterating by manually installing packages from source every time `renv::restore` crashes), but these increase the complexity considerably to be considered common advice. I spent a few hours trying to restore my environment and I did not succeed. Hours is a scale of time that should be spent doing science, not trying to install your environment.


My previous experience with [Julia's `Pkg.jl`](https://jkrumbiegel.com/pages/2022-08-26-pkg-introduction/), [which provides a very good experience](https://blog.devgenius.io/the-most-underrated-feature-of-the-julia-programming-language-the-package-manager-652065f45a3a) and the [julia general registry](https://github.com/JuliaRegistries/General?tab=readme-ov-file#how-do-i-remove-a-package-or-version-from-the-registry) tell me that things can and should be better.


* Interestingly enough,for Mac and Windows the thing seem to be better as historical binaries are available for all the packages as well.
