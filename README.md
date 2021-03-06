
<!-- README.md is generated from README.Rmd. Please edit that file -->

# conflr

[![Travis build
status](https://travis-ci.org/line/conflr.svg?branch=master)](https://travis-ci.org/line/conflr)

conflr is an R package to post [R
Markdown](https://rmarkdown.rstudio.com/) documents to
[Confluence](https://www.atlassian.com/software/confluence), a content
collaboration tool by Atlassian.

## Installation

``` r
devtools::install_github("line/conflr")
```

## Preparation

Set `CONFLUENCE_URL` to the Confluence endpoint in `.Renviron` (you can
open the file with `usethis::edit_r_environ()`).

    CONFLUENCE_URL=https://confluence.example.com

## Usage

### 1\. Move focus to the .Rmd file and click “Post to Confluence” Addin

(**Caution for those who are not familiar with R Markdown**: R
Markdown’s powerfulness allows you to execute arbitrary codes; be sure
about what the code does before clicking “Post to Confluence”\!)

![](./man/figures/screenshot1.png)

![](./man/figures/screenshot2.png)

### 2\. Check the preview and click “Publish”

  - **type**: page or blogpost
  - **Space Key**: key for the space
  - **Parent page ID**: (optional) page ID to which the new page will
    belong

![](./man/figures/screenshot3.png)

### 3\. Check the result

![](./man/figures/screenshot4.png)

## Usage in console

``` r
library(conflr)

# list pages
res <- confl_list_pages(spaceKey = "foo")
purrr::map_chr(res$results, "id")

# get page info
page <- confl_get_page(res$results[[2]]$id)
page$title

# create a page
new_page <- confl_post_page(
  spaceKey = "foo",
  title = "Test",
  body = glue::glue(
    '<ac:structured-macro ac:name="code">
     <ac:plain-text-body><![CDATA[this is my code]]></ac:plain-text-body>
     </ac:structured-macro>
    '))
new_page$`_links`
```

## How to contribute

See [CONTRIBUTING.md](CONTRIBUTING.md)

## License

    Copyright (C) 2019 LINE Corporation
    
    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, version 3.
    
    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
    
    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

See [LICENSE.md](LICENSE.md) for more detail.
