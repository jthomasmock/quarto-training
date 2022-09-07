## RStudio Pro

- Auto-enabled in RStudio Pro

## Jupyter/VSCode

- Add to $PATH via `.bashrc`
- In RStudio, go to home directory
  - Enable Hidden Files with Files pane > More > Show Hidden Files
  - Open `.bashrc`

Add:

```bash
# this will add Quarto to $PATH on VSCode + Jupyter
export PATH="$PATH:/usr/lib/rstudio-server/bin/quarto/bin"
```