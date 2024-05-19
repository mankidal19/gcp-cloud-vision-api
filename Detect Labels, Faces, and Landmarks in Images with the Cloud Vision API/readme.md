# Task 4. Label detection

```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
```

# Task 5. Web detection

```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request-web.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} > response-web.json
```