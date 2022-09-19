
## Publishing

[RStudio Connect User Guide -
Quarto](https://docs.rstudio.com/connect/user/quarto/)

[Quarto - Publishing to RStudio
Connect](https://quarto.org/docs/publishing/rstudio-connect.html#overview)

<table style="width:99%;">
<colgroup>
<col style="width: 60%" />
<col style="width: 25%" />
<col style="width: 13%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Tool</th>
<th style="text-align: left;">Method</th>
<th style="text-align: left;">Supported Runtimes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><a
href="https://docs.rstudio.com/connect/user/publishing/#publishing-documents">RStudio
IDE</a></td>
<td style="text-align: left;">Push-button publishing</td>
<td style="text-align: left;"><code>knitr</code>,
<code>jupyter</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><a
href="https://quarto.org/docs/publishing/rstudio-connect.html">The
<code>quarto</code> CLI</a></td>
<td style="text-align: left;"><code>quarto publish connect</code></td>
<td style="text-align: left;"><code>knitr</code>,
<code>jupyter</code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a
href="https://quarto-dev.github.io/quarto-r/">The <code>quarto</code> R
package</a></td>
<td
style="text-align: left;"><code>quarto_publish_[site|app|doc]()</code></td>
<td style="text-align: left;"><code>knitr</code>,
<code>jupyter</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><a
href="https://docs.rstudio.com/connect/user/publishing-r/#quarto">The
<code>rsconnect</code> R package</a></td>
<td
style="text-align: left;"><code>deployApp(quarto = QUARTO_PATH)</code>,<br />
<code>writeManifest(quarto = QUARTO_PATH)</code></td>
<td style="text-align: left;"><code>knitr</code>,
<code>jupyter</code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a
href="https://docs.rstudio.com/connect/user/publishing-cli-quarto/">The
<code>rsconnect-python</code> CLI</a></td>
<td
style="text-align: left;"><code>rsconnect deploy quarto</code>,<br />
<code>rsconnect write-manifest quarto</code></td>
<td style="text-align: left;"><code>jupyter</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><a
href="https://docs.rstudio.com/connect/user/publishing-cli-manifest/">The
<code>rsconnect-python</code> CLI</a></td>
<td
style="text-align: left;"><code>rsconnect deploy manifest</code></td>
<td style="text-align: left;"><code>knitr</code>,
<code>jupyter</code></td>
</tr>
</tbody>
</table>

## Push-Button

- Possible via RStudio or Jupyter Notebook

## `rsconnect` Package/CLI

- with `rsconnect` R package make sure to reference
  `quarto = QUARTO_PATH`

  - You can get this from terminal via: `which quarto` or in R via
    `quarto::quarto_path()`

- with `rsconnect` Python CLI, use `rsconnect deploy quarto` - indicates
  Quarto content

- Requires an API token - [generate from RStudio
  Connect](https://docs.rstudio.com/connect/user/api-keys/)

## Connecting to Connect

### From R

Make sure you are using a recent version of `quarto`/`rsconnect` R
packages.

``` r
# quarto v1.2
# rsconnect v0.8.27
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

Make sure you’re on a recent version of `rsconnect-python` (2022-09-19
is
[v1.10](https://colorado.rstudio.com/rspm/client/#/repos/14/packages/rsconnect-python))

``` bash
pip install rsconnect
# if needing to upgrade
# pip install --upgrade rsconnect-python
```

Check existing servers:

``` bash
rsconnect list
```

Connect yourself to Connect

``` bash
rsconnect add --server https://colorado.rstudio.com/rsc/ --name colorado --api-key $CONNECT_API_KEY
```

Deploy a doc

``` bash
rsconnect deploy quarto some.qmd
```

## Publishing from Version Control (github)

- Create a manifest file
- Check it into version control along with the source code/files

``` r
rsconnect::writeManifest(
  appFiles = "test-deploy.qmd",
  quarto = quarto::quarto_path()
)
```

``` bash
rsconnect write-manifest quarto FILE_OR_PROJECT
```
