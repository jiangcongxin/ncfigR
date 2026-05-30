<p align="center">
  <img src="man/figures/ncfigR-banner.svg" alt="ncfigR banner" width="100%">
</p>

# ncfigR

`ncfigR` 是一个轻量 R 包，用于从整理好的 source-data 表格生成生信论文常用图形面板。它适合单细胞、空间组学、细胞通讯、轨迹分析和方法 benchmark 图，不依赖大型对象，也不替代 Seurat / Scanpy 的完整分析流程。

## 有什么用

- 把 `embedding.tsv`、`marker_matrix.tsv`、`lr_pairs.tsv`、`trajectory.tsv` 等表格快速画成论文图。
- 统一 UMAP、组成柱状图、marker heatmap、LR heatmap、网络图、trajectory 和 benchmark 图的风格。
- 用 `patchwork` 组合多 panel 主图。
- 一次性导出 PDF、SVG、PNG，便于投稿、PPT 和后期编辑。

## 安装

```r
install.packages("remotes")
remotes::install_github("jiangcongxin/ncfigR")
```

## 最小示例

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

fig <- compose_nc_figure(list(p1, p2), ncol = 2)

export_figure_bundle(fig, "example_figure", out_dir = "figures/exports")
```

## 主要函数

|函数|用途|
|---|---|
| `plot_embedding_panel()` | UMAP / embedding 散点图 |
| `plot_composition_panel()` | 细胞组成柱状图 |
| `plot_marker_heatmap()` | marker heatmap |
| `plot_lr_heatmap()` | ligand-receptor heatmap |
| `plot_lr_network()` | ligand-receptor 网络图 |
| `plot_trajectory_trend()` | pseudotime / trajectory 趋势图 |
| `plot_benchmark_heatmap()` | 方法比较 heatmap |
| `compose_nc_figure()` | 组合多 panel 图 |
| `export_figure_bundle()` | 导出 PDF、SVG、PNG |

## 示例数据

包内置了 toy source-data 表格：

```r
system.file("extdata", package = "ncfigR")
```

真实项目建议把分析结果整理成同类 tidy table，再传入对应函数。

## 许可证

MIT License.
