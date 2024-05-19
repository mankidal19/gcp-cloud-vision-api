# Task 4. Call the text detection method

```
curl -s -X POST -H "Content-Type: application/json" --data-binary @ocr-request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o ocr-response.json
```

Note: For images with more text, the Cloud Vision API also has a DOCUMENT_TEXT_DETECTION feature. This response includes additional information and breaks text down into page, blocks, paragraphs, and words.

# Task 5. Send text from the image to the Translation API

## Run this Bash command in Cloud Shell to extract the image text from the previous step and copy it into a new translation-request.json (all in one command):

```
STR=$(jq .responses[0].textAnnotations[0].description ocr-response.json) && STR="${STR//\"}" && sed -i "s|your_text_here|$STR|g" translation-request.json
```

## Now you're ready to call the Translation API. This command will also copy the response into a translation-response.json file:

```
curl -s -X POST -H "Content-Type: application/json" --data-binary @translation-request.json https://translation.googleapis.com/language/translate/v2?key=${API_KEY} -o translation-response.json
```

# Task 6. Analyzing the image's text with the Natural Language API

## Run this Bash command in Cloud Shell to copy the translated text into the content block of the Natural Language API request:

```
STR=$(jq .data.translations[0].translatedText  translation-response.json) && STR="${STR//\"}" && sed -i "s|your_text_here|$STR|g" nl-request.json
```

## Call the analyzeEntities endpoint of the Natural Language API with this curl request:

```
curl "https://language.googleapis.com/v1/documents:analyzeEntities?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @nl-request.json
```
