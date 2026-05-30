# ncfigR

`ncfigR` is a small R package for making publication-style bioinformatics figure panels from tidy source-data tables.

It is designed for single-cell, spatial omics, communication, trajectory, and benchmark figures where the plotting inputs should be easy to audit and reuse.

## What it does

- Draw UMAP / embedding panels with stable palettes.
- Draw cell composition panels.
- Draw marker and ligand-receptor heatmaps.
- Draw simple ligand-receptor network panels.
- Draw trajectory trend panels.
- Draw method benchmark heatmaps.
- Combine panels with `patchwork`.
- Export PDF, SVG, and PNG bundles.

## Installation

```r
install.packages("remotes")
remotes::install_github("jiangcongxin/ncfigR")
```

## Quick example

```r
library(ncfigR)
library(readr)

embedding <- read_tsv(
  system.file("extdata/embedding.tsv", package = "ncfigR"),
  show_col_types = FALSE
)

composition <- read_tsv(
  system.file("extdata/composition.tsv", package = "ncfigR"),
  show_col_types = FALSE
)

p1 <- plot_embedding_panel(
  embedding,
  color_col = "cell_type",
  label = TRUE,
  title = "Cell states"
)

p2 <- plot_composition_panel(
  composition,
  group_col = "group",
  category_col = "cell_type",
  value_col = "proportion",
  title = "Cell composition"
)

fig <- compose_nc_figure(
  list(p1, p2),
  ncol = 2,
  title = "Example ncfigR figure"
)

export_figure_bundle(fig, "example_figure", out_dir = "figures/exports")
```

## Main functions

| Function | Use |
|---|---|
| `plot_embedding_panel()` | UMAP / embedding scatter panel |
| `plot_composition_panel()` | Cell composition bar plot |
| `plot_marker_heatmap()` | Marker heatmap |
| `plot_lr_heatmap()` | Ligand-receptor heatmap |
| `plot_lr_network()` | Ligand-receptor network panel |
| `plot_trajectory_trend()` | Pseudotime / trajectory trend panel |
| `plot_benchmark_heatmap()` | Benchmark metric heatmap |
| `compose_nc_figure()` | Combine panels into a multi-panel figure |
| `export_figure_bundle()` | Export PDF, SVG, PNG, and optional source manifest |

## Data format

The package works best with tidy tables. Example files are included under:

```r
system.file("extdata", package = "ncfigR")
```

These toy files are only used to demonstrate plotting functions. Real projects should pass their own audited source-data tables.

## License

MIT License.
