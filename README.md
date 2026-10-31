# YOLO26 driver behavior model artifacts

This repository contains **model weights, aggregate evaluation results, and a validation report only**. It excludes source code, credentials, raw images, individual annotations, driver identifiers, and per-image predictions.

## Original driver behavior classifier

`original/model.pt` is a YOLO26n-cls checkpoint for the State Farm c0–c9 image classes. It was evaluated once on 2,557 images from three held-out drivers. Test accuracy: 82.13%; macro F1: 83.03%. Input preparation uses RGB full-frame aspect-preserving letterbox to 224×224 followed by division by 255. Class names and full-precision metrics are in `original/metrics.json`.

## New handheld-object pilot

`handheld-pilot/model.pt` is a YOLO26n detector fine-tuned on manually drawn phone, cup, and other-handheld-object boxes. Its driver-disjoint pilot split contains only 56 training and 15 validation images. Validation box mAP@0.5 is 0.758; box mAP@0.5:0.95 is 0.444. This **does not establish real-world accuracy**. The original locked test drivers were not used.

## New annotated detector

`annotated/model.pt` is a YOLO26n detector trained on the second LabelImg round for phone, cup, other handheld object, and five head-direction boxes. It used 677 training images from 14 drivers and 148 validation images from 3 different drivers. Validation box mAP@0.5 is 0.619; mAP@0.5:0.95 is 0.376. See `annotated/validation_report.html` for per-class counts and metrics. Twenty-five images without saved labels were excluded, and the remaining manifest rows were not marked fully reviewed. `up` has only five training boxes and `TurnL` has 21; these classes are not reliable enough for real-world claims. The locked original test drivers were not used.

The original classifier and both detectors solve different tasks, so their metrics should not be ranked against each other. Bounding boxes are not human keypoints or left/right hand occupancy labels.

The weights are Ultralytics YOLO models; check the applicable [Ultralytics license](https://www.ultralytics.com/license) before redistribution or commercial use. No training images or annotation files are included.
