# MRI SynthSR

SynthSR can generate a synthetic 1 mm isotropic T1‑weighted scan with high image homogeneity from virtually any medical imaging modality, regardless of contrast or resolution (e.g., T2‑weighted MRI, CT scans).

The [original code](https://github.com/BBillot/SynthSR) depended on outdated libraries and was limited to Python 3.7. The [updated version](https://github.com/freesurfer/freesurfer/tree/dev/mri_synthsr) is distributed as part of FreeSurfer, which currently does not support modern operating systems such as Ubuntu 24.04. It ships with Python 3.8 and can be difficult to run with GPU acceleration in containerized environments. In addition, the FreeSurfer package is subject to a restrictive license and requires a local license file.

This repository provides a minimal, standalone installation of SynthSR. It removes unused dependencies, updates libraries to modern versions, and eliminates the need for FreeSurfer or its licensing. The code retains full attribution and the original permissive Apache open‑source license. The name has been changed from `mri_synthsr` to `py_synthsr` to avoid naming conflicts with FreeSurfer distributions, but the models and operation should be equivalent.

## Installation and Usage

From the source directory:

```bash
# Download the model files into the package's models folder
curl -L https://osf.io/download/jqdcm/ -o models.zip \
  && unzip -jo models.zip -d py_synthsr/models \
  && rm models.zip
# Install the package into your current Python environment
pip install .

# Run SynthSR on an example FLAIR image
py_synthsr --i FLAIR.nii.gz --o FLAIR2T1w.nii.gz
```

## Limitations

 - At the time of writing, [TensorFlow](https://pypi.org/project/tensorflow/) does not support Python versions later than 3.12.
 - This package includes updates to work with recent TensorFlow releases, but results may differ slightly from the original. Limited testing shows >99% of voxels are identical; for 8‑bit outputs, no voxel differed by more than 1.

## Citation

Iglesias JE, Billot B, Balbastre Y, Tabari A, Conklin J, RG Gonzalez, Alexander DC, Golland P, Edlow B, Fischl B ([2021](https://www.sciencedirect.com/science/article/pii/S1053811921004833)) Joint super-resolution and synthesis of 1 mm isotropic MP-RAGE volumes from clinical MRI exams with scans of different orientation, resolution and contrast. NeuroImage. 15:237:118206 [PMID: 34048902](https://pubmed.ncbi.nlm.nih.gov/34048902/).