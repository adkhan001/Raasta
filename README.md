# Raasta · Flooded-road intelligence

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adkhan001/Raasta/blob/main/Raasta_Colab.ipynb)
![Framework](https://img.shields.io/badge/PyTorch-U--Net-EE4C2C)
![Task](https://img.shields.io/badge/task-semantic%20segmentation-159b8d)
![Status](https://img.shields.io/badge/status-research%20prototype-amber)

**Detect flooded roads from paired before-and-after satellite images, train in Google Colab, and keep datasets and checkpoints in Google Drive.**

Built by **Allah Ditta**. Raasta explores flood-response mapping through remote sensing and deep learning. It is a research prototype, with Pakistan as a potential future validation context—not a validated operational system.

## What goes in and what comes out?

| Input | Output |
| --- | --- |
| Overlapping before/after georeferenced, 8-bit RGB GeoTIFFs | Three-class pixel segmentation: background, road with no flood label, flooded road |
| Saved held-out test example | Prediction overlay, model scores, and accuracy against reference labels |
| Your own image pair | Overlay and uncalibrated confidence; accuracy requires reference labels |

Outputs include PNG previews, georeferenced class and score rasters, JSON summaries, and downloadable ZIP files.

## Features

- Six-channel U-Net in PyTorch: before RGB + after RGB.
- Official SpaceNet 8 file discovery, paired-image download, alignment and road-mask preparation.
- Persistent raw imagery, processed samples, model checkpoints and results in Google Drive.
- Resume training across Colab sessions.
- In-notebook interface for selecting test examples or uploading imagery.
- Held-out evaluation: pixel accuracy, balanced accuracy, precision, recall, F1 and IoU.
- Geographic prediction visualization.
- A separate **synthetic** inspection-planning experiment; it is not a real road-routing system.

## Run in Google Colab

1. Click **Open in Colab** above and save a copy to your Drive.
2. Select a GPU runtime when available.
3. Run installation and configuration. Keep `USE_DRIVE=True` and `RESUME=True`.
4. Use the `starter` profile for an initial experiment. The `smoke` profile is a functionality check and may lack enough examples of each class.
5. Run discovery, preprocessing, training and evaluation in order.
6. Run the interface near the end of the notebook. Choose a test example or upload a before/after image pair, then click **Run prediction**.
7. Run the final cell and click **Evaluate model accuracy** for held-out model metrics.

The notebook installs missing supporting packages and uses Colab's PyTorch installation. GPU availability and runtime duration depend on your Colab session. Dataset downloads require internet access and sufficient Drive storage; the default download guard is 6 GB.

### Continue tomorrow

Run installation and configuration with the same settings. Set `CONTINUE_PREVIOUS=True` in the session-restoration cell and run it. Then continue at training, evaluation or the interface. Avoid rerunning model-definition cells after restoration, since they initialize a new model.

| Saved item | Default location |
| --- | --- |
| Raw downloaded dataset | `MyDrive/Raasta/dataset/raw/` |
| Prepared samples | `MyDrive/Raasta/dataset/cache_v1/` |
| Checkpoints and metrics | `MyDrive/Raasta/runs/raasta_v1_starter/` |
| Interface predictions | Run folder → `ui_predictions/` |

The notebook is code; it does not contain the downloaded dataset or trained weights.

## Dataset and provenance

Raasta uses **SpaceNet 8**, a historical flood-mapping dataset with Germany and Louisiana imagery and annotations. Downloads come from the official SpaceNet dataset bucket; the notebook records selected files in its manifest. This is not a live Pakistan imagery feed.

- [SpaceNet 8 dataset and challenge](https://www.spacenet.ai/sn8-challenge/)
- [Official baseline repository](https://github.com/SpaceNetChallenge/SpaceNet8)
- [Hänsch et al., SpaceNet 8 — The Detection of Flooded Roads and Buildings, 2022](https://openaccess.thecvf.com/content/CVPR2022W/EarthVision/papers/Hansch_SpaceNet_8_-_The_Detection_of_Flooded_Roads_and_Buildings_CVPRW_2022_paper.pdf)

Retain the provider's attribution and follow its dataset license when redistributing imagery or derived data. The notebook identifies the dataset as CC BY-SA 4.0; consult the provider for authoritative terms. No third-party imagery is redistributed in this repository.

## Evaluation and honest reporting

**No headline accuracy is claimed in this repository.** Train and evaluate your run to obtain measured results.

Pixel accuracy can be inflated by background pixels. Compare it with the background-only baseline, balanced accuracy and per-class road/flood metrics. Per-image accuracy is measured only where reference labels exist. Softmax confidence is an uncalibrated model score, not a probability that a road is safe.

The model's compact architecture, subset selection and buffered road masks are educational design choices; results are not an official SpaceNet benchmark reproduction. Report the run profile, checkpoint epoch and held-out metrics alongside any public demonstration.

## Limitations and next steps

- Historical data does not establish present-day road conditions.
- Pakistan performance has not been validated.
- RGB images can be affected by clouds, shadows, appearance changes and alignment errors.
- Road masks use buffered annotations rather than measured road widths.
- Predictions do not establish road passability or suitability for emergency routing.
- Next steps: dated local imagery and labels, geographic transfer evaluation, score calibration and a real connected road graph.

## Contributing

Useful contributions include reproducible bug reports, image-alignment checks, geographic generalization experiments and evaluation improvements. Describe your Colab runtime, profile and error when opening an issue. Do not upload credentials, private imagery or personal Drive contents.

**Topics:** flood detection · satellite imagery · remote sensing · semantic segmentation · geospatial AI · disaster response · PyTorch · Google Colab · SpaceNet 8
