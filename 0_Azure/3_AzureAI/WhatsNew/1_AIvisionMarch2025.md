# ​What's new in Azure AI Vision?​ - March 2025 Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-12-24

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What is Azure AI Vision?](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview)
- [What is Image Analysis?](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-image-analysis?tabs=4-0)
- [What is the Azure AI Face service?](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-identity)
- [What is Video Analysis?](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/intro-to-spatial-analysis-public-preview?tabs=sa)

</details>

## Services Overview 

<details>
<summary>Optical Character Recognition (OCR)</summary>

> Extracts text from images. You can use the Read API to extract printed and handwritten text from photos and documents. It is used to recognize and convert texts, helping with text on various surfaces and backgrounds. These include business documents, invoices, receipts, posters, business cards, letters, and whiteboards. The OCR APIs support extracting printed text in several languages.

- **API Endpoint**: The request to the endpoint should include the image data either as a URL or as binary data in the request body. Endpoint format: `/vision/v3.2/read/analyze`
- **Input Formats**: JPEG, PNG, BMP, PDF (for multi-page documents)
- **Output**: JSON with detected text and bounding boxes
- **Languages Supported**: Multiple languages including English, Spanish, French, German, Chinese, Japanese, and more.
- **Response Structure**: The JSON response includes an array of `readResults`, each containing:
  - **Page**: The page number (for multi-page documents).
  - **Language**: The detected language of the text.
  - **Angle**: The rotation angle of the text.
  - **Width and Height**: Dimensions of the image.
  - **Lines**: An array of detected lines of text, each with:
    - **BoundingBox**: Coordinates of the text line.
    - **Text**: The recognized text.
    - **Words**: An array of words within the line, each with its own bounding box and text.
- **Error Handling**: The API provides detailed error messages for issues such as unsupported file formats, corrupted images, or exceeding size limits.
- **Performance**: The OCR service is optimized for speed and accuracy, capable of processing large volumes of images quickly.

> Follow the [OCR quickstart](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/quickstarts-sdk/client-library?tabs=windows%2Cvisual-studio&pivots=programming-language-python) to get started.

</details>

<img width="550" alt="img" src="https://github.com/user-attachments/assets/2aa93951-91a9-4b63-add0-34a3b94f533d">

From [OCR official documentation](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-ocr)

<details>
<summary>Image Analysis</summary>

> Extracts many visual features from images, such as objects, faces, adult content detection, and auto-generated tags for identification.

- **API Request**: The request to the endpoint should include the image data either as a URL or as binary data in the request body. Endpoint format: `/vision/v3.2/analyze`
- **Response Structure**: The JSON response includes an array of `categories`, `tags`, `objects`, `faces`, `color`, and `imageType`, each containing:
  - **Categories**: Classifies images into predefined categories. An array of categories with `name` and `score` indicating the confidence level.
  - **Tags**: Identifies objects, living beings, scenery, and actions. An array of tags with `name` and `confidence` score.
  - **Objects**: Provides coordinates for objects within an image. An array of detected objects with `rectangle` coordinates and `object` name.
  - **Faces**: Detects faces and provides attributes like age, gender, and emotion. An array of detected faces with `age`, `gender`, `faceRectangle`, and `emotion`.
  - **Color**: Determines dominant colors. Information about the dominant colors, accent color, and whether the image is black & white.
  - **ImageType**: Identifies whether an image is a photograph, clipart, or line drawing. Details about the image type, such as whether it is a clipart or line drawing.
- **Text Extraction (OCR)**: Extracts printed and handwritten text.
- **Output**: JSON with detected features and their details.
- **Error Handling**: The API provides detailed error messages for issues such as unsupported file formats, corrupted images, or exceeding size limits.
- **Performance**: The Image Analysis service is optimized for speed and accuracy, capable of processing large volumes of images quickly.

> Follow the [Image Analysis quickstart](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/quickstarts-sdk/image-analysis-client-library-40?tabs=visual-studio%2Cwindows&pivots=programming-language-python) to get started.

</details>

| Generate image captions	| Tag visual features	| Background removal (v4.0 preview only) | 
| ----- | ----- | ---- | 
| <img width="550" alt="img" src="https://github.com/user-attachments/assets/9150c064-9392-451a-9398-2b5a8428a0be"> | <img width="550" alt="img" src="https://github.com/user-attachments/assets/3530b5a8-b42d-47b7-87d6-3659271124e5"> | <img width="550" alt="img" src="https://github.com/user-attachments/assets/69c2c7f8-f959-443d-b950-a994aa91eaaa"> |

From [official documentation](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-image-analysis?tabs=4-0)

<details>
<summary>Face</summary>
  
> Provides AI algorithms that detect, recognize, and analyze human faces in images. Facial recognition software can be important in many different scenarios such as identifying people in photos or videos or finding a particular individual among a large group of people.

- **API Endpoint**: `/face/v1.0/detect`
- **API Request**: The request to the endpoint should include the image data either as a URL or as binary data in the request body. The request can also specify which features to analyze using query parameters.
  - **Parameters**:
    - `returnFaceId`: Boolean to specify if face IDs should be returned.
    - `returnFaceLandmarks`: Boolean to specify if face landmarks should be returned.
    - `returnFaceAttributes`: Comma-separated string to specify which face attributes to return (e.g., `age,gender,emotion`).
- **Features**:
  - **Face Detection**: Identifies human faces and provides bounding boxes.
  - **Face Recognition**: Matches detected faces against a database of known faces.
  - **Face Verification**: Compares two faces to determine if they belong to the same person.
  - **Face Grouping**: Groups similar faces together.
  - **Face Attributes**: Provides detailed attributes like age, gender, emotion, head pose, facial hair, and accessories.
- **Output**: JSON with detected faces and their attributes.
- **Response Structure**: The JSON response includes an array of detected faces, each containing:
  - **FaceId**: Unique identifier for the detected face.
  - **FaceRectangle**: Coordinates of the bounding box around the face.
  - **FaceLandmarks**: (Optional) Detailed coordinates of facial landmarks.
  - **FaceAttributes**: (Optional) Detailed attributes of the face, including:
    - `age`: Estimated age of the person.
    - `gender`: Gender of the person.
    - `emotion`: Detected emotions with confidence scores.
    - `headPose`: Orientation of the head.
    - `facialHair`: Presence of facial hair.
    - `glasses`: Type of glasses worn.
    - `accessories`: Detected accessories like headwear.
    - `blur`: Blur level of the image.
    - `exposure`: Exposure level of the image.
    - `noise`: Noise level of the image.
- **Error Handling**: The API provides detailed error messages for issues such as unsupported file formats, corrupted images, or exceeding size limits. Common error codes include:
  - `InvalidImageFormat`: The provided image format is not supported.
  - `InvalidImageSize`: The provided image exceeds the size limit.
  - `FaceNotFound`: No faces were detected in the image.
- **Performance**: The Face API is optimized for speed and accuracy, capable of processing large volumes of images quickly. It supports high concurrency and provides low-latency responses.

> Follow the [Face quickstart](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/quickstarts-sdk/identity-client-library?tabs=windows%2Cvisual-studio&pivots=programming-language-csharp) to get started.

</details>

<img width="550" alt="img" src="https://github.com/user-attachments/assets/dd3b303a-ec5f-4f89-bbc3-3a362b8174b1">

From [official documentation](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-identity)

<details>
<summary>Video Analysis</summary>

> Includes video-related features like [Spatial Analysis](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/spatial-analysis-container?tabs=azure-stack-edge) and [Video Retrieval](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/how-to/video-retrieval). Spatial analysis analyzes real-time footage captured by cameras in relation to predefined areas of interest or rules set by users for specific actions or events within a video feed and produces events accordingly when rules are met.

- **API Endpoint**: `/video/v1.0/analyze`
- **API Request**: The request to the endpoint should include the video data either as a URL or as binary data in the request body. The request can also specify which features to analyze using query parameters.
  - **Parameters**:
    - `spatialAnalysis`: Boolean to specify if spatial analysis should be performed.
    - `peopleCounting`: Boolean to specify if people counting should be performed.
    - `movementTracking`: Boolean to specify if people movement tracking should be performed.
    - `zoneMonitoring`: Boolean to specify if zone monitoring should be performed.
    - `lineCrossingDetection`: Boolean to specify if line crossing detection should be performed.
    - `customEvents`: Boolean to specify if custom events should be defined and detected.
- **Features**:
  - **Spatial Analysis**: Monitors and analyzes movements and interactions within physical spaces.
  - **People Counting**: Counts the number of people in a designated area.
  - **People Movement Tracking**: Tracks the movement of individuals within a space.
  - **Zone Monitoring**: Detects when people enter or exit specific zones.
  - **Line Crossing Detection**: Detects when people cross predefined lines.
  - **Custom Events**: Defines custom events based on spatial criteria.
- **Output**: JSON with detected events and their details.
- **Response Structure**: The JSON response includes an array of detected events, each containing:
  - **EventId**: Unique identifier for the detected event.
  - **EventType**: Type of the detected event (e.g., `PeopleCounting`, `ZoneMonitoring`).
  - **Timestamp**: Time at which the event was detected.
  - **Details**: Detailed information about the event, including:
    - `count`: Number of people detected (for people counting).
    - `coordinates`: Coordinates of detected movements or zone entries/exits.
    - `lineCrossed`: Information about the line crossed (for line crossing detection).
    - `customEventDetails`: Details about custom events defined by the user.
- **Error Handling**: The API provides detailed error messages for issues such as unsupported file formats, corrupted videos, or exceeding size limits. Common error codes include:
  - `InvalidVideoFormat`: The provided video format is not supported.
  - `InvalidVideoSize`: The provided video exceeds the size limit.
  - `EventNotDetected`: No events were detected in the video.
- **Performance**: The Video Analysis service is optimized for speed and accuracy, capable of processing large volumes of video data quickly. It supports high concurrency and provides low-latency responses.

</details>

> E.g People counting: 

https://github.com/user-attachments/assets/eb7be305-b61e-45b7-8a3c-4d9378b7d99f 

> E.g Social distancing and face mask detection: 

https://github.com/user-attachments/assets/cd8f4f18-5cfe-43c6-865e-0480021d699e 

From [official documentation](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/intro-to-spatial-analysis-public-preview?tabs=sa)

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
