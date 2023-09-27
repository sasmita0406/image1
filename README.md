# image1
import json
from ibm_watson import VisualRecognitionV4
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from ibm_watson.visual_recognition_v4 import FileWithMetadata

# Replace with your API key and endpoint
api_key = 'YOUR_API_KEY'
endpoint = 'YOUR_ENDPOINT'
classifier_id = 'YOUR_CLASSIFIER_ID'  # You can use 'default' for the default classifier

# Initialize the Visual Recognition client
authenticator = IAMAuthenticator(api_key)
visual_recognition = VisualRecognitionV4(
    version='2021-06-07',
    authenticator=authenticator
)
visual_recognition.set_service_url(endpoint)

# Path to the image you want to recognize
image_path = 'path_to_your_image.jpg'

# Perform image recognition
with open(image_path, 'rb') as image_file:
    response = visual_recognition.classify(
        images_file=FileWithMetadata(image_file),
        classifier_ids=[classifier_id],
        threshold='0.6'  # Adjust the confidence threshold as needed
    ).get_result()

# Print the results
print(json.dumps(response, indent=2))
print(json.dumps(response, indent=2))
