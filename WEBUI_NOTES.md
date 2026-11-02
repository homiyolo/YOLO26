# Local WebUI model selection and pose drawing

The local DriveLab WebUI now has a separate **识别模型** selector on the **实时摄像头** page. It lists the original behavior classifier and the preliminary annotated detector. You can switch while the camera is running; the next frame uses the newly selected model, and results from a previous selection are ignored. Detection mode draws target boxes on the live view.

This repository does not publish the WebUI source code under the owner's privacy preference. The feature is available in the owner's local project at `http://127.0.0.1:8765/` after refreshing the page. Model weights and aggregate validation results remain available in this repository.

The annotated detector is preliminary. In particular, the `up` and `TurnL` classes have few reviewed examples, and its boxes do not represent body keypoints or definitive driver actions.

## Body-pose view

The image, video, and live camera pages also list **人体姿态关键点（预训练）** when the local project contains the official `yolo26n-pose.pt` checkpoint. Selecting it draws COCO 17 body landmarks and skeleton edges. An analyzed image can be downloaded with its overlay; a video produces an annotated MP4 and a CSV with keypoint coordinates; the camera displays the skeleton over the live view. Confidence thresholds remain adjustable on each page.

This checkpoint was not fine-tuned or validated on the State Farm cabin images. It does not estimate finger joints, hand occupancy, held objects, driver actions, or head rotation angles. Occluded body landmarks may be absent. The official pose model and task description are available in the [Ultralytics pose documentation](https://docs.ultralytics.com/tasks/pose/).

The WebUI implementation and private driver images remain only on the owner's computer. This public repository provides no WebUI source code or individual pose predictions.

## Local video upload update

The local DriveLab video page accepts files up to 800 MB, including H.264 (`avc1`) encoded `.mp4` files. Uploads stream to local disk and are decoded for inference; annotated previews are encoded as browser-playable H.264 MP4. The WebUI source and uploaded videos remain private on the owner's computer.

The video results page now includes a seekable timeline. Scrubbing to a time displays and downloads an annotated PNG frame from the local preview. The displayed recognition label is the most recent sampled prediction at or before that time; unsampled frames do not run an additional inference pass.
