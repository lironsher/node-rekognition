# node-rekognition
AWS Rekognition library

## Installation
    npm install node-rekognition

## Use

### Instantiation
```javascript
const Rekognition = require('node-rekognition')

// Set your AWS credentials
const AWSParameters = {
    "accessKeyId": "XXX",
    "secretAccessKey": "XXX",
    "region": "XXX",
    "bucket": "XXX"
}

const rekognition = new Rekognition(AWSParameters)
```

### Upload images to S3
Some methods from AWS Rekognition need one or more images uploaded to AWS S3 bucket
```javascript
/**
 * Upload image or images array to S3 bucket into specified folder
 * 
 * @param {Array.<string>|string} imagePaths 
 * @param {string} folder a folder name inside your AWS S3 bucket (it will be created if not exists)
 */
const s3Images = await rekognition.uploadToS3(imagePaths, folder)
```

### detectLabels
```javascript
/**
 * Detects instances of real-world labels within an image 
 * 
 * @param {Object} s3Image 
 * @param {string} threshold (optional. Defaults 50)
 */
const imageLabels = await rekognition.detectLabels(s3Image)
```

### detectFaces
```javascript
/**
 * Detects faces within an image
 * 
 * @param {Object} s3Image
 */
const imageFaces = await rekognition.detectFaces(s3Image)
```

### compareFaces
```javascript
/**
 * Compares a face in the source input image with each face detected in the target input image
 * 
 * @param {Object} sourceS3Image 
 * @param {Object} targetS3Image 
 * @param {string} threshold (optional. Defaults 90)
 */
const faceMatches = await rekognition.compareFaces(sourceS3Image, targetS3Image, threshold)
```

### detectModerationLabels
```javascript
/**
 * Detects explicit or suggestive adult content in image
 * 
 * @param {Object} s3Image
 * @param {number} threshold (optional. Defaults 50)
 */
const moderationLabels = await rekognition.detectModerationLabels(s3Image, threshold)
```

### createCollection
```javascript
/**
 * Creates a collection 
 * 
 * @param {string} collectionId 
 */
const collection = await rekognition.createCollection(collectionId)
```

### indexFaces
```javascript
/**
 * Detects faces in the input image and adds them to the specified collection
 * 
 * @param {string} collectionId 
 * @param {Object} s3Image
 */
const facesIndexed = await rekognition.indexFaces(collectionId, s3Image)
```

### listFaces
```javascript
/**
 * List the metadata for faces indexed in the specified collection
 * 
 * @param {string} collectionId 
 */
const faces = await rekognition.listFaces(collectionId)
```

### searchFaces
```javascript
/**
 * Searches in the collection for matching faces of faceId
 * 
 * @param {string} collectionId 
 * @param {string} faceId 
 * @param {number} threshold (optional. Defaults 90)
 */
const faceMatches = await rekognition.searchFacesByFaceId(collectionId, faceId, threshold)
```

### searchFacesByImage
```javascript
/**
 * First detects the largest face in the image (indexes it), and then searches the specified collection for matching faces.
 * 
 * @param {string} collectionId 
 * @param {Object} s3Image 
 * @param {number} threshold (optional. Defaults 90)
 */
const faceMatches = await rekognition.searchFacesByImage(collectionId, s3Image, threshold)
```

## Test
First of all, you must create a *parameters.json* file and set your AWS parameters. You have an example file *parametrs.json.example*
- cp parameters.json.example parameters.json
- vim parameters.json

Then:
- npm install
- npm test

## Requirements
node >= 7.10.0

## Contributing
**You are welcome contribute via pull requests.**

## More info about AWS Rekognition
http://docs.aws.amazon.com/rekognition/latest/dg/API_Operations.html
http://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Rekognition.html