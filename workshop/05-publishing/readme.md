## Publishing

[RStudio Connect User Guide - Quarto](https://docs.rstudio.com/connect/user/quarto/) 

[Quarto - Publishing to RStudio Connect](https://quarto.org/docs/publishing/rstudio-connect.html#overview)

+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+
| Tool                                                                                         | Method                                | Supported Runtimes |
+:=============================================================================================+:======================================+:===================+
| [RStudio IDE](https://docs.rstudio.com/connect/user/publishing/#publishing-documents)        | Push-button publishing                | `knitr`, `jupyter` |
+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+
| [The `quarto` CLI](https://quarto.org/docs/publishing/rstudio-connect.html)                  | `quarto publish connect`              | `knitr`, `jupyter` |
+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+
| [The `quarto` R package](https://quarto-dev.github.io/quarto-r/)                             | `quarto_publish_[site|app|doc]()`     | `knitr`, `jupyter` |
+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+
| [The `rsconnect` R package](https://docs.rstudio.com/connect/user/publishing-r/#quarto)      | `deployApp(quarto = QUARTO_PATH)`,\   | `knitr`, `jupyter` |
|                                                                                              | `writeManifest(quarto = QUARTO_PATH)` |                    |
+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+
| [The `rsconnect-python` CLI](https://docs.rstudio.com/connect/user/publishing-cli-quarto/)   | `rsconnect deploy quarto`,\           | `jupyter`          |
|                                                                                              | `rsconnect write-manifest quarto`     |                    |
+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+
| [The `rsconnect-python` CLI](https://docs.rstudio.com/connect/user/publishing-cli-manifest/) | `rsconnect deploy manifest`           | `knitr`, `jupyter` |
+----------------------------------------------------------------------------------------------+---------------------------------------+--------------------+

## Push-Button

- Possible via RStudio or Jupyter Notebook

## `rsconnect` Package/CLI

-   with `rsconnect` R package make sure to reference `quarto = QUARTO_PATH`

    -   You can get this from terminal via: `which quarto` or in R via `quarto::quarto_path()`

-   with `rsconnect` Python CLI, use `rsconnect deploy quarto` - indicates Quarto content



## Connecting to Connect

### From R

Make sure you are using a recent version of `quarto`/`rsconnect` R packages.

```r
install.packages(c("quarto", "rsconnect"))
```

Check existing accounts:

``` r
rsconnect::accounts()
#> rsconnect::accounts()
#>                 name                         server
#> 1             thomas           colorado.rstudio.com
```

Connect yourself to Connect

``` r
rsconnect::connectApiUser(
  server="connect.mydomain.com",
  account="myusername",
  apiKey="micOXRF89vCQgEr1DovGQMyhmsASz1sf"
    )
```

Deploy a doc

``` r
rsconnect::deployDoc(
  "test-deploy.qmd", 
  quarto = quarto::quarto_path(),
  account = "thomas",
  server = "colorado.rstudio.com"
  )
```

### From Python

Make sure you're on a recent version of `rsconnect-python` (2022-09-19 is [v1.10](https://colorado.rstudio.com/rspm/client/#/repos/14/packages/rsconnect-python))
```bash
pip install rsconnect
# if needing to upgrade
# pip install --upgrade rsconnect-python
```

Check existing servers:

```bash
rsconnect list
```

Connect yourself to Connect

```bash
rsconnect add --server https://colorado.rstudio.com/rsc/ --name colorado --api-key $CONNECT_API_KEY
```

Deploy a doc

```bash
rsconnect deploy quarto some.qmd
```

## Publishing from Version Control (github)

- Create a manifest file
- Check it into version control along with the source code/files

```r
rsconnect::writeManifest(
  appFiles = "test-deploy.qmd",
  quarto = quarto::quarto_path()
)
```

```bash
rsconnect write-manifest quarto FILE_OR_PROJECT
```