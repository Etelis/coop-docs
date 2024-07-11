---
title: PDFGenerator
layout: page
parent: Functions
grand_parent: Backend
---

# PDFGenerator Function

The `PDFGenerator` function is designed to generate PDF reports for users based on their game data stored in MongoDB. This function handles HTTP POST requests and creates PDFs, which are then uploaded to Google Cloud Storage.

## URL to Activate

To activate the function, send a POST request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/PDFGenerator-1](https://europe-central2-co-op-world-game.cloudfunctions.net/PDFGenerator-1)

## Input

The function expects a JSON payload with the user IDs. Below is an example of the expected input:

```json
{
    "user_ids": ["user_123", "user_456", "user_789"]
}
```

## Output

The function returns a response with the URL to the generated zip file containing PDFs:

- **Success (200 OK)**: `{"url": "https://storage.googleapis.com/your_bucket/your_file.zip"}`
- **Error (500 Internal Server Error)**: `{"error": "Error message"}` or other relevant error messages.

## Functions

- **initialize_mongodb()**: Initializes the MongoDB client and connects to the database.
- **build_cors_response(response, status_code=200)**: Builds a response with CORS headers.
- **fetch_image(url, width=50, height=65)**: Fetches an image from a URL and returns it as an Image object for the PDF.
- **generate_pdf_report(user_id, documents)**: Generates a PDF report for a user based on their game data.
- **generate_and_upload_pdfs(request)**: Main function to generate PDFs and upload them to Google Cloud Storage.

## Example Request

```bash
curl -X POST   https://europe-central2-co-op-world-game.cloudfunctions.net/PDFGenerator-1   -H 'Content-Type: application/json'   -d '{
        "user_ids": ["user_123", "user_456", "user_789"]
      }'
```

This cloud function is part of the Administrator panel and will generate PDFs based on the specified format for every user under an instructor.
