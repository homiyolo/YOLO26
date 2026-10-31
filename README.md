# YOLO26 driver behavior model artifacts

This repository contains **model weights and aggregate evaluation results only**. It excludes source code, credentials, raw images, individual annotations, driver identifiers, and per-image predictions.

## Original driver behavior classifier

`original/model.pt` is a YOLO26n-cls checkpoint for the State Farm c0–c9 image classes. It was evaluated once on 2,557 images from three held-out drivers. Test accuracy: 82.13%; macro F1: 83.03%. Input preparation uses RGB full-frame aspect-preserving letterbox to 224×224 followed by division by 255. Class names and full-precision metrics are in `original/metrics.json`.

## New handheld-object pilot

`handheld-pilot/model.pt` is a YOLO26n detector fine-tuned on manually drawn phone, cup, and other-handheld-object boxes. Its driver-disjoint pilot split contains only 56 training and 15 validation images. Validation box mAP@0.5 is 0.758; box mAP@0.5:0.95 is 0.444. This **does not establish real-world accuracy**. The original locked test drivers were not used.

Head-direction labels are currently too sparse (one `TurnL`, two `up`) for a meaningful head-pose detector or fair model comparison. The original model and the pilot detector solve different tasks, so their metrics should not be ranked against each other. The original model remains the supported behavior classifier.

The weights are Ultralytics YOLO models; check the applicable [Ultralytics license](https://www.ultralytics.com/license) before redistribution or commercial use. No training images or annotation files are included.

