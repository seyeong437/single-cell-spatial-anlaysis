# Single-cell and spatial analysis notebooks

Learning notebooks for single-cell RNA-seq and spatial omics analysis in Python, built while preparing to study the tumour immune microenvironment and immunotherapy response.

Each notebook follows an official [Scanpy](https://scanpy.readthedocs.io) or [Squidpy](https://squidpy.readthedocs.io) tutorial, with my own explanations, checks and adaptations for current package versions. The first cell of each notebook gives its aim, data, workflow and expected output.

## Notebooks

| # | Notebook | Topics |
|---|---|---|
| 1 | Preprocessing and clustering (PBMC 3k) | QC, normalisation, clustering, marker genes, cell-type annotation |
| 2 | Core plotting | Dot plots, violin plots, heatmaps, differential expression |
| 3 | Data integration | Reference mapping (ingest), batch correction (BBKNN) |
| 4 | Trajectory inference | PAGA, diffusion pseudotime, gene changes along differentiation paths |
| 5 | Cell-cycle scoring | Gene-set scoring, regressing out cell-cycle effects |
| 6 | Visium H&E (spatial transcriptomics) | Image features, neighbourhood enrichment, co-occurrence, ligand-receptor analysis, Moran's I |
| 7 | Imaging mass cytometry | Single-cell spatial statistics, interaction matrix, network centrality |
| 8 | MIBI-TOF | Per-cell marker intensities from raw images and segmentation masks, arcsinh transformation |
| 9 | Xenium (human lung cancer) | SpatialData, Xenium-specific QC, clustering, spatial statistics, plotting on the tissue image |

## Notes and adaptations
- Trajectory inference: Louvain could not be installed, so Leiden was used; clusters were re-identified with marker genes and differentiation paths redefined.
- Data integration: BBKNN was run with `computation="cKDTree"` to avoid a faulty `annoy` installation.
- Core plotting: thin, offset violin plots (seaborn 0.13) were fixed with `dodge=False`.
- Visium H&E: `scale` in `calculate_image_features` changes the crop resolution, not the surrounding context; `spot_scale` widens the crop.
- Xenium: the current 10x data release (162,254 cells × 377 genes, multimodal cell segmentation) differs from the tutorial's (161,000 × 480), so QC distributions, cluster numbers and top Moran's I genes differ. Hard-coded values (cluster "12", genes AREG and MET) were replaced with this dataset's own, and the final plot was updated for current `spatialdata-io` and `spatialdata-plot` (`render_labels` on `cell_labels`).

## Environment
Python 3.12 (Scanpy notebooks) and 3.13 (Squidpy notebooks), Scanpy 1.12.4, Squidpy 1.8.3. Full package list in `requirements.txt`.
Most datasets are downloaded by the notebooks and are not stored in this repository.
The Xenium dataset must be downloaded manually from 10x Genomics ("FFPE Human Lung Cancer with Xenium Multimodal Cell Segmentation", Output Bundle). No data are stored in this repository.

## Next

## Next
A personal project applying these methods to public melanoma imaging mass cytometry data, focusing on T cells and immunotherapy response.
