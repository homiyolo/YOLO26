# Local WebUI camera model selection

The local DriveLab WebUI now has a separate **识别模型** selector on the **实时摄像头** page. It lists the original behavior classifier and the preliminary annotated detector. You can switch while the camera is running; the next frame uses the newly selected model, and results from a previous selection are ignored. Detection mode draws target boxes on the live view.

This repository does not publish the WebUI source code under the owner's privacy preference. The feature is available in the owner's local project at `http://127.0.0.1:8765/` after refreshing the page. Model weights and aggregate validation results remain available in this repository.

The annotated detector is preliminary. In particular, the `up` and `TurnL` classes have few reviewed examples, and its boxes do not represent body keypoints or definitive driver actions.
