[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/brain-life/abcd-spec)
[![brainlife.io/app](https://img.shields.io/badge/brainlife.io-app-green.svg)](https://brainlife.io/app/5f3593e84615e04651bf9364)
[![DOI:10.25663/brainlife.app.399](https://img.shields.io/badge/DOI-10.25663%2Fbrainlife.app.399-blue)](https://doi.org/10.25663/brainlife.app.399)

# app-C-PAC-brainlife.io
This is an app to run [**C-PAC: Configurable Pipeline for the Analysis of Connectomes**](https://fcp-indi.github.io/docs/latest/user) [via brainlife.io]((https://brainlife.io/app/5f3593e84615e04651bf9364)).

This app:
1. gets the latest C-PAC Singularity image
2. converts given [anat/t1w](https://brainlife.io/datatype/58c33bcee13a50849b25879a) and [func/task](https://brainlife.io/datatype/59b685a08e5d38b0b331ddc5) ([brainlife.io datatypes](https://brainlife.io/docs/user/datatypes)) to [BIDS](https://bids-specification.readthedocs.io/en/stable/) (the data structure required by C-PAC)
3. runs C-PAC, persisting the working directory
     * with a [preconfigured pipeline](https://fcp-indi.github.io/docs/latest/user/preconfig) given the optional `preconfig` [configuration parameter](https://brainlife.io/docs/apps/register/#configuration-parameters)
     * with the [default pipeline](https://fcp-indi.github.io/docs/latest/user/preconfig#default-the-default-pipeline) otherwise

### Authors
- [The C-PAC Team](https://fcp-indi.github.io/docs/latest/user/#the-c-pac-team)

### Contributors
- [Soichi Hayashi](https://github.com/soichih)
- [Franco Pestilli](https://github.com/francopestilli)
- [Giulia Bertò](https://github.com/giulia-berto)
- [Brad Caron](https://github.com/bacaron)

### Funding Acknowledgements
brainlife.io is publicly funded and for the sustainability of the project it is helpful to acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your publications and code reusing this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

See also [C-PAC's funding acknowledgements](https://fcp-indi.github.io/docs/latest/user/#funding-acknowledgements)

### Citations
We kindly ask that you cite the following articles when publishing papers and code using this code.

1. Avesani, P., McPherson, B., Hayashi, S., et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Sci Data 6*, 69 (2019). [doi:10.1038/s41597-019-0073-y](https://dx.doi.org/10.1038/s41597-019-0073-y)
2. Craddock C., Sikka S., Cheung B., et al. Towards Automated Analysis of Connectomes:
The Configurable Pipeline for the Analysis of Connectomes (C-PAC). *Front. Neuroinform*. Conference Abstract:
Neuroinformatics 2013 (2013). [doi:10.3389/conf.fninf.2013.09.00042](https://dx.doi.org/10.3389/conf.fninf.2013.09.00042)


## Running the App

### On Brainlife.io

You can run this App online at [doi:10.25663/brainlife.app.399](https://doi.org/10.25663/brainlife.app.399) via the "Execute" tab.

### Running Locally (on your machine)

C-PAC is a BIDS app, so it requires a BIDS directory. This brainlife.io app expects that BIDS directory to be a directory called `bids` in the same directory as the `main` script.

1. `git clone` this repo.
2. Copy (`cp -r /path/to/bids_dir ./bids`) or link (`cp -al /path/to/bids/dir ./bids`) a BIDS directory to a directory called `bids` within the cloned directory.
3. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.
    ```json
    {
      "preconfig": "fmriprep-options"
    }
    ```
    At this point, your directory structure should look like
    ```tree
    .
    ├── bids
    |   └── …
    ├── config.json
    ├── LICENSE
    ├── main
    └── README.md
    ```
4. Launch the App by executing `main`
    ```bash
    ./main
    ```

#### Simulating brainlife.io locally

1. `git clone` this repo.
2. If you don't have your own Brainlife input file, you can download sample datasets from Brainlife.io, or you can use [Brainlife CLI](https://github.com/brain-life/cli) (again, in the cloned directory).
    ```BASH
    npm install -g brainlife
    bl login
    bl dataset download 5e93e694aa1f998a35ac4d22
    bl dataset download 5e56f2220f7fa621dd3cd1b7
    ```
3. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files. Brainlife generates this config file automatically based on your selections in the web GUI.
    ```json
    {
      "t1": "./5e93e694aa1f998a35ac4d22/t1.nii.gz",
      "bold": "./5e56f2220f7fa621dd3cd1b7/bold.nii.gz",
      "preconfig": "fmriprep-options",
      "_inputs": [
        {
          "id": "t1",
          "datatype": "58c33bcee13a50849b25879a",
          "meta": {
            "subject": "10",
            "RepetitionTime": 3,
            "TaskName": "Viewing alternating blocks presenting either ready-to-eat edible objects or pictures of items unrelated to food",
            "MagneticFieldStrength": 3,
            "Manufacturer": "GE",
            "ManufacturersModelName": "DISCOVERY_MR750",
            "SoftwareVersions": "23_LX_MR_Software_release:DV22.0_V02_1122.a",
            "SeriesDescription": "fmri_2d_epi_condition_1",
            "ScanningSequence": "EP_GR",
            "SequenceVariant": "SS",
            "ScanOptions": "SAT_GEMS_EPI_GEMS_ACC_GEMS_FS",
            "ImageType": ["ORIGINAL", "PRIMARY", "EPI", "NONE"],
            "SliceThickness": 3,
            "SpacingBetweenSlices": 3,
            "EchoTime": 0.03,
            "FlipAngle": 90,
            "PhaseEncodingPolarityGE": "Flipped",
            "CoilString": "32Ch_Head",
            "PercentPhaseFOV": 100,
            "AcquisitionMatrixPE": 64,
            "ReconMatrixPE": 64,
            "EffectiveEchoSpacing": 0.000468,
            "TotalReadoutTime": 0.029484,
            "PixelBandwidth": 7812.5,
            "PhaseEncodingDirection": "j",
            "SliceTiming": [0,1.5,0.06,1.56,0.12,1.62,0.18,1.68,0.24,1.74,0.3,1.8,0.36,1.86,0.42,1.92,0.48,1.98,0.54,2.04,0.6,2.1,0.66,2.16,0.72,2.22,0.78,2.28,0.84,2.34,0.9,2.4,0.96,2.46,1.02,2.52,1.08,2.58,1.14,2.64,1.2,2.7,1.26,2.76,1.32,2.82,1.38,2.88,1.44,2.94],
            "InPlanePhaseEncodingDirectionDICOM": "COL",
            "task": "viewingfoodlowres",
            "dim":[3,160,192,128,1,1,1,1],
            "pixdim":[1,1,1.3333330154418945,1.3333330154418945,1,0,0,0]
          },
          "tags": [],
          "datatype_tags": [],
          "subdir": "5e93e694aa1f998a35ac4d22",
          "dataset_id": "5e93e694aa1f998a35ac4d22",
          "project": "5d64733db29ac960ca2e797f",
          "task_id": "5f861c7bc7adcbb6ae137fe1",
          "keys": [
            "t1"
          ]
        },
        {
          "id": "func",
          "datatype": "59b685a08e5d38b0b331ddc5",
          "meta": {
            "AcquisitionDateTime": "2017-04-13T11:48:43.116000",
            "EchoTime": 0.0352,
            "EffectiveEchoSpacing": 0.000580013,
            "FlipAngle": 56,
            "ImageType": ["ORIGINAL","PRIMARY","M","MB","ND","MOSAI"],
            "MagneticFieldStrength": 3,
            "Manufacturer": "Siemens",
            "ManufacturersModelName": "Prisma",
            "PhaseEncodingDirection": "j-",
            "RepetitionTime": 0.955,
            "SliceTiming": [0.875,0.795,0.715,0.635,0.5575,0.4775,0.3975,0.3175,0.2375,0.1575,0.08,0,0.875,0.795,0.715,0.635,0.5575,0.4775,0.3975,0.3175,0.2375,0.1575,0.08,0,0.875,0.795,0.715,0.635,0.5575,0.4775,0.3975,0.3175,0.2375,0.1575,0.08,0,0.875,0.795,0.715,0.635,0.5575,0.4775,0.3975,0.3175,0.2375,0.1575,0.08,0,0.875,0.795,0.715,0.635,0.5575,0.4775,0.3975,0.3175,0.2375,0.1575,0.08,0],
            "TaskName": "rest",
            "TotalReadoutTime": 0.0580013,
            "subject": "10",
            "task": "rest"
          },
          "tags": ["task-rest"],
          "datatype_tags": ["rest"],
          "subdir": "5e56f2220f7fa621dd3cd1b7",
          "dataset_id": "5e56f2220f7fa621dd3cd1b7",
          "project": "5d64733db29ac960ca2e797f",
          "task_id": "5f861c7bc7adcbb6ae137fe1",
          "keys": ["bold"]
        }
      ]
    }
    ```

4. Launch the App by executing `main`
    ```bash
    ./main
    ```


## Output

A C-PAC output directory and a C-PAC working directory. See [Check Your Outputs](https://fcp-indi.github.io/docs/latest/user/output_dir) and [Output Settings](https://fcp-indi.github.io/docs/latest/user/output_config) for detailed information about C-PAC's outputs.

### Dependencies

This App requires
* [brainlife](https://www.npmjs.com/package/brainlife)
* [Singularity](https://www.sylabs.io/singularity/)
* [bl2bids](https://github.com/brainlife/abcd-spec/blob/master/hooks/bl2bids)
* [jq](https://stedolan.github.io/jq)

All of these dependencies are available on brainlife.io.

## Issues and troubleshooting

### Limitations

#### Pipelines
Currently this app only runs preconfigured pipelines. Please see the documentation for [Pre-configured Pipelines](https://fcp-indi.github.io/docs/latest/user/preconfig) to see the available pipelines.

#### C-PAC version
Currently this app only runs [the latest version](https://fcp-indi.github.io/docs/latest/user/release_notes/latest) of C-PAC.

### Bug reports and feature requests

If you run into an issue, please check [existing bug reports](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues?q=is%3Aissue+is%3Aopen+label%3Abug).

If a bug report already exists for your issue, please add a :+1: and/or add any new information you have that might help us resolve the issue.

If a bug report does not exist yet, please [open one using our bug report template](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues/new?assignees=&labels=bug%2C+user-reported&template=bug_report.md&title=%F0%9F%90%9B+%5BUser-reported+Bug%5D), filling out as much detail as you can.

If you want to request a feature, we also have [a template to create a feature request](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues/new?assignees=&labels=enhancement%2C+user-reported&template=feature_request.md&title=%E2%9C%A8+%5BUser-requested+Feature%5D).

#### brainlife.io:  [MIT Copyright © 2020 brainlife.io The University of Texas at Austin and Indiana University](./LICENSE)
#### C-PAC: [BSD 3-Clause "New" or "Revised" License © 2016–2020 Child Mind Institute, Inc. and C-PAC developers](https://github.com/FCP-INDI/C-PAC/blob/master/LICENSE)
