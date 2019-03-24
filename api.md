# API Overview
インストールを行うと、edgetpu モジュールがインストールされます。このモジュールはTensorflow Lite モデルに対するハイレベルなAPIを提供します。



These APIs are pre-installed on the Dev Board. If you're using the USB Accelerator, you must download the API onto the host that's connected to the USB Accelerator (see the USB Accelerator setup guide).

Key APIs from the library that perform inferencing are the following:

ClassificationEngine:
Performs image classification. Just instantiate an instance by specifying a model, and then pass an image (such as a JPEG) to `ClassifyWithImage(self, img, threshold=0.1, top_k=0.3, resample=Image.NEAREST)`
and it returns a list of labels and scores.

DetectionEngine:
Performs object detection. Just instantiate an instance by specifying a model, and then pass an image (such as a JPEG) to
`DetectWithImage(self, img, threshold=0.1, top_k=0.3, relative_coord=True, resample=Image.NEAREST)`
and it returns a list of DetectionCandidate objects, which each contain a label, a score, and the coordinates of the object.

BasicEngine:
The base class for the other two. It provides several other methods inherited by each.

The ClassificationEngine and DetectionEngine support all image formats supported by Pillow (including JPEG, PNG, BMP), but they must be in RGB color space (no transparency).

Additionally, we've included an API that performs on-device transfer learning:

ImprintingEngine:
This class implements a transfer-learning technique called imprinting that does not require backward propagation, allowing you to perform model retraining that's accelerated on the Edge TPU (only for image classification models). For more information about this API, read Retrain an image classification model on-device.
Much more detail about the APIs is available in the Edge TPU API Reference (ZIP download).

