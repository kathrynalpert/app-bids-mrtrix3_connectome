# BIDS Mrtrix3 Connectome

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Builds a subject structural connectome from DWI and a T1-weighted image with the MRtrix3_connectome BIDS App (0.2.2), with optional dwipreproc preprocessing and an AAL or FreeSurfer parcellation.**

Arranges the T1w and one or more DWI runs into a BIDS directory and runs the bids/mrtrix3_connectome participant-level pipeline (MRtrix3 tractography and connectome construction) with the chosen parcellation and streamline count. Use it to obtain a tractography-based connectome from raw or preprocessed DWI in one step. Running the built-in preprocessing (preprocessed unchecked) needs at least two DWI runs whose metadata include TotalReadoutTime and PhaseEncodingDirection. The whole BIDS App output directory is returned as a raw dataset.

| | |
|---|---|
| 📥 **Inputs** | `neuro/dwi` · `neuro/anat/t1w` |
| 📤 **Outputs** | `raw` |
| 🐳 **Container** | `katealpert/bids-mrtrix3_connectome` |
| ⚙️ **Resources** | 8 CPUs · 24 h walltime |
| 🔗 **Run it** | [doi.org/10.25663/bl.app.77](https://doi.org/10.25663/bl.app.77) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `dwi` | `neuro/dwi` | yes | One or more DWI runs (with bvals and bvecs) of the subject; multiple runs become run-01, run-02, ... in the BIDS input. For preprocessing, at least two runs with TotalReadoutTime and PhaseEncodingDirection in the metadata. |
| `t1` | `neuro/anat/t1w` | yes | T1-weighted anatomical image of the same subject. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `mrtrix3_connectome` | `raw` | The MRtrix3_connectome participant output directory (connectome matrices and intermediate files) for the subject. |

<details>
<summary><b>⚙️ Parameters</b> (3)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `streamlines` | number |  | The number of streamlines to generate |
| `parcellation` | enum | `aal` | Connectome parcellation scheme Options: `aal`, `aal2`, `fs_2005`, `fs_2009`. |
| `preprocessed` | boolean | `true` | Uncheck this to run mrtrix3 dwipreproc. To do so, you must have at least 2 DWI inputs and your metadata must contain both TotalReadoutTime and PhaseEncodingDirection. |

</details>

<!-- brainlife-app:end -->

