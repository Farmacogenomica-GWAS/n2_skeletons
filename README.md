# n2_skeletons File Processing

This document describes the processing of the `n2_skeletons.hdf5` file using Python and the `h5py`, `pandas`, and `numpy` libraries. The primary goal was to extract all datasets from the file, including those within groups, and convert them into individual CSV files. Special attention was paid to reshaping multi-dimensional datasets into a 2D format suitable for CSV storage and extracting scalar data from the 'provenance\_tracking' group. The `n2_skeletons.hdf5` file was obtained by using the Tierpsy Tracker and contains information related to worm morphology and movement.

**Key Steps:**

1.  **File Inspection:** The `n2_skeletons.hdf5` file was inspected to identify its top-level datasets and groups. The names and sizes of the top-level datasets were printed to the console.
2.  **Dataset Extraction and Export:** All datasets within the HDF5 file, including those nested within groups, were processed and exported to individual CSV files.
    * **Reshaping:** Datasets with more than two dimensions were reshaped into a 2D array (`(number_of_records, flattened_features)`) before being saved to CSV. The original shape of these reshaped datasets was noted during the export process.
    * **Filename Convention:** For datasets within groups, the group name was included in the CSV filename, with '/' replaced by '\_' to avoid directory issues (e.g., `intensity_analysis/switched_head_tail` was saved as `intensity_analysis_switched_head_tail.csv`).
3.  **Scalar Data from 'provenance\_tracking':** Scalar datasets found within the 'provenance\_tracking' group were specifically extracted and saved into a single CSV file named `provenance_tracking_scalars.csv`. This file contains the name and value of each scalar dataset.

4.  **Output Format:** Each extracted dataset was saved as a separate CSV file. For multi-dimensional datasets, the data was flattened into a 2D structure. Scalar data from 'provenance\_tracking' was stored in a key-value pair format in `provenance_tracking_scalars.csv`.

5.  **Visualization of the datasets:** The first 5 rows of each generated CSV file were printed to the console to provide a quick overview of the extracted data.

**Top-Level Datasets Extracted:**

* `blob_features`
* `contour_area`
* `contour_side1` (reshaped to 2D)
* `contour_side1_length`
* `contour_side2` (reshaped to 2D)
* `contour_side2_length`
* `contour_width`
* `plate_worms`
* `skeleton` (reshaped to 2D)
* `skeleton_length`
* `trajectories_data`
* `width_midbody`

**Datasets Extracted from Groups:**

* `intensity_analysis/switched_head_tail` (saved as `intensity_analysis_switched_head_tail.csv`)
* `timestamp/raw` (saved as `timestamp_raw.csv`)
* `timestamp/time` (saved as `timestamp_time.csv`)

**Scalar Data from 'provenance\_tracking':**

* Extracted and saved to `provenance_tracking_scalars.csv` (includes `BLOB_FEATS`, `INT_SKE_ORIENT`, `SKE_CREATE`, `SKE_FILT`, `SKE_INIT`, `SKE_ORIENT`, `TRAJ_CREATE`, `TRAJ_JOIN`).

**Libraries Used:**

* `h5py`: For reading and navigating the HDF5 file structure, accessing datasets and groups.
* `pandas`: For creating and exporting DataFrames to CSV files and for displaying the first few rows.
* `numpy`: Used for reshaping multi-dimensional arrays.
* `os`: For handling file paths and directory creation.

**Purpose:**

The processing steps outlined here were performed to extract all relevant data from the `n2_skeletons.hdf5` file into a more manageable CSV format. This includes handling the complexities of multi-dimensional datasets by reshaping them and specifically extracting scalar metadata. The resulting CSV files are intended to facilitate further analysis of worm behavior and morphology. Visualizing the first few rows of each output CSV provides a quick verification of the extraction process.
