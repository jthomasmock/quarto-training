## Reports

### Themes

set with YAML `theme: name`

- default
- cerulean
- cosmo
- cyborg
- darkly
- flatly
- journal
- litera
- lumen
- lux
- materia
- minty
- morph
- pulse
- quartz
- sandstone
- simplex
- sketchy
- slate
- solar
- spacelab
- superhero
- united
- vapor
- yeti
- zephyr

### Tabsets

Pandoc divs:

```
::: {.panel-tabset}

## Tab 1

... content

## Tab 2

... content

:::
```

### Figure Layout

Layout options:
  - `layout-ncol: 2` and `layout-nrow: 2`
  - `layout: "[[70,30], [100]]"
  
Works for images:

```{r}
#| layout-ncol: 2
#| fig-cap: 
#|   - "Speed and Stopping Distances of Cars"
#|   - "Vapor Pressure of Mercury as a Function of Temperature"

plot(cars)
plot(pressure)
```

and for text:

::: {layout-ncol=2}
- Item X
- Item Y
- Item Z

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur gravida eu erat et fring. Morbi congue augue vel eros ullamcorper, eget convallis tortor sagittis. Fusce sodales viverra mauris a fringilla. Donec feugiat, justo eu blandit placerat, enim dui volutpat turpis, eu dictum lectus urna eu urna. Mauris sed massa ornare, interdum ipsum a, semper massa. 
:::

## Presentations

### Themes

Set in YAML woth `theme: name`

- beige
- blood
- dark
- default
- league
- moon
- night
- serif
- simple
- sky
- solarized

### Incremental 

- Pandoc div 
  - `::: {.incremental}`
  - YAML and `incremental: true`
  - Turn off with `::: {.nonincremental}`

- Pandoc span
  - `[some text]{.fragment}`
  
### Columns

```cide
:::: {.columns}

::: {.column width="50%"}
contents...
:::

::: {.column width="50%"}
contents...
:::

::::
```