# Kidney Stone Detection in CT Images (academic prototype)

## Dataset (inspected from the supplied ZIP)
Roboflow export `TEZ_ROI_AUG` v3 (CC BY 4.0): `data.yaml`, `README.roboflow.txt`, `README.dataset.txt`, `train/`, `valid/`, `test/` (each with `images/` and `labels/`).
- Annotations: YOLO bounding boxes (5 values per line); one class, `Tas_Var` (stone present)
- Images: JPG, 391x320. Train 1,054 (2x Roboflow-augmented copies of 532 source images), valid 123, test 123
- 2,827 boxes in total; 1 empty label file; no stone-negative images
- No segmentation masks, DICOM files, pixel spacing, patient IDs or reference measurements

## What is implemented
YOLOv8 detector, evaluation on valid/test (precision, recall, F1, mAP), false-positive/false-negative analysis,
pixel-based box measurements, Plotly dashboard, Gradio app (single and batch, CSV export), weight saving/reloading.

## Not implemented (data cannot support it)
Segmentation / Dice / IoU against masks, millimetre size, 3D volume, ROC-AUC, Grad-CAM, DICOM input.

## Run
1. Open `kidney_stone_detection.ipynb` in Google Colab, set Runtime > GPU, then Run all.
2. Upload the dataset ZIP when prompted.
3. Training saves `kidney_stone_best.pt`; the notebook also writes `metrics.json`, `dashboard.html` and a bundle ZIP.
4. The last Gradio cell prints a link. Upload one or several PNG/JPG/TIFF images.

## Test new images in Python
    from kidney_stone_app import run_batch
    summary, details, gallery, csv_path = run_batch(["my_ct.png"], "kidney_stone_best.pt")

## Missing data that blocks full size estimation
Segmentation masks, pixel spacing or DICOM headers, slice spacing, reference measurements in mm, patient IDs, stone-negative images.

Academic research prototype. Not for clinical use.
