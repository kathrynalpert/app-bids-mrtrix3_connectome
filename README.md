<h1 align="center">BIDS Mrtrix3 Connectome</h1>

<p align="center">
  Builds a subject structural connectome from DWI and a T1-weighted image with the MRtrix3_connectome BIDS App (0.2.2), with optional dwipreproc preprocessing and an AAL or FreeSurfer parcellation.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/bl.app.77"><img src="https://img.shields.io/badge/Brainlife-bl.app.77-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Builds a subject structural connectome from DWI and a T1-weighted image with the MRtrix3_connectome BIDS App (0.2.2), with optional dwipreproc preprocessing and an AAL or FreeSurfer parcellation.**

Arranges the T1w and one or more DWI runs into a BIDS directory and runs the bids/mrtrix3_connectome participant-level pipeline (MRtrix3 tractography and connectome construction) with the chosen parcellation and streamline count. Use it to obtain a tractography-based connectome from raw or preprocessed DWI in one step. Running the built-in preprocessing (preprocessed unchecked) needs at least two DWI runs whose metadata include TotalReadoutTime and PhaseEncodingDirection. The whole BIDS App output directory is returned as a raw dataset.

| | |
|---|---|
| **Inputs** | `neuro/dwi` · `neuro/anat/t1w` |
| **Outputs** | `raw` |
| **Container** | `katealpert/bids-mrtrix3_connectome` |
| **Resources** | 8 CPUs · 24 h walltime |
| **Run it** | [doi.org/10.25663/bl.app.77](https://doi.org/10.25663/bl.app.77) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `dwi` | `neuro/dwi` | yes | One or more DWI runs (with bvals and bvecs) of the subject; multiple runs become run-01, run-02, ... in the BIDS input. For preprocessing, at least two runs with TotalReadoutTime and PhaseEncodingDirection in the metadata. |
| `t1` | `neuro/anat/t1w` | yes | T1-weighted anatomical image of the same subject. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `mrtrix3_connectome` | `raw` | The MRtrix3_connectome participant output directory (connectome matrices and intermediate files) for the subject. |

<details>
<summary><b>Parameters</b> (3)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `streamlines` | number |  | The number of streamlines to generate |
| `parcellation` | enum | `aal` | Connectome parcellation scheme Options: `aal`, `aal2`, `fs_2005`, `fs_2009`. |
| `preprocessed` | boolean | `true` | Uncheck this to run mrtrix3 dwipreproc. To do so, you must have at least 2 DWI inputs and your metadata must contain both TotalReadoutTime and PhaseEncodingDirection. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/bl.app.77](https://doi.org/10.25663/bl.app.77), choose `neuro/dwi`, `neuro/anat/t1w` from your project, set the parameters and press **Execute**. The results are saved to your project as `raw`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `katealpert/bids-mrtrix3_connectome`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "bvals": "/path/to/dwi/bvals",
       "bvecs": "/path/to/dwi/bvecs",
       "dwi": "/path/to/dwi/dwi",
       "t1": "/path/to/t1/t1",
       "streamlines": "",
       "parcellation": "aal",
       "preprocessed": true
   }
   ```

3. Run `./main`.

## Troubleshooting

- **Two DWI images are required to run mrtrix3_connectome preprocessing.**: Provide at least two DWI runs, or keep preprocessed checked.
- **TotalReadoutTime and PhaseEncodingDirection BIDS fields reqd to run mrtrix3_connectome preproc.**: Add TotalReadoutTime and PhaseEncodingDirection to the DWI metadata, or keep preprocessed checked.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- BIDS Mrtrix3 Connectome. brainlife.io App. [doi:10.25663/bl.app.77](https://doi.org/10.25663/bl.app.77)
- Fischl. FreeSurfer. *NeuroImage* 62:774-781 (2012). [doi:10.1016/j.neuroimage.2012.01.021](https://doi.org/10.1016/j.neuroimage.2012.01.021)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Tournier et al. MRtrix3: A fast, flexible and open software framework for medical image processing and visualisation. *NeuroImage* 202:116137 (2019). [doi:10.1016/j.neuroimage.2019.116137](https://doi.org/10.1016/j.neuroimage.2019.116137)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

Maintained by [@kathrynalpert](https://github.com/kathrynalpert).
