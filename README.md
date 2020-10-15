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

1. git clone this repo.
2. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.

```json
{
  "t1": "./59a5f2a1c1e7111a78d11a51/t1.nii.gz",
  "bold": "./59cc5342f45e7344b8c8afe5/bold.nii.gz",
  "preconfig": "fmriprep-options"
}
```

3. Launch the App by executing `main`

```bash
./main
```

### Sample Datasets

If you don't have your own input file, you can download sample datasets from Brainlife.io, or you can use [Brainlife CLI](https://github.com/brain-life/cli) (again, in the cloned directory).

```
npm install -g brainlife
bl login
bl dataset download 59a5f2a1c1e7111a78d11a51
bl dataset download 59cc5342f45e7344b8c8afe5
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
Currently this app only runs preconfigured pipelines. Please see the documentation for [Pre-configured Pipelines](https://fcp-indi.github.io/docs/latest/user/preconfig) to see the available pipelines. The default pipeline is [consistently erroring](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues/2#issuecomment-702209732) at the moment.

#### C-PAC version
Currently this app only runs [the latest version](https://fcp-indi.github.io/docs/latest/user/release_notes/latest) of C-PAC.

### Bug reports and feature requests

If you run into an issue, please check [existing bug reports](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues?q=is%3Aissue+is%3Aopen+label%3Abug).

If a bug report already exists for your issue, please add a :+1: and/or add any new information you have that might help us resolve the issue.

If a bug report does not exist yet, please [open one using our bug report template](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues/new?assignees=&labels=bug%2C+user-reported&template=bug_report.md&title=%F0%9F%90%9B+%5BUser-reported+Bug%5D), filling out as much detail as you can.

If you want to request a feature, we also have [a template to create a feature request](https://github.com/FCP-INDI/app-C-PAC-brainlife.io/issues/new?assignees=&labels=enhancement%2C+user-reported&template=feature_request.md&title=%E2%9C%A8+%5BUser-requested+Feature%5D).

#### brainlife.io:  [MIT Copyright © 2020 brainlife.io The University of Texas at Austin and Indiana University](./LICENSE)
#### C-PAC: [BSD 3-Clause "New" or "Revised" License © 2016–2020 Child Mind Institute, Inc. and C-PAC developers](https://github.com/FCP-INDI/C-PAC/blob/master/LICENSE)
