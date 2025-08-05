## Task: 
1. Navigate to url: <WEB_FORM_URL>
2. Go to Digital Downloads page
3. Extract the list of all products along with their prices and target urls
4. Save the extracted data in both Markdown and JSON formats
   * File Name: `digital-downloads.md`
   * File Name: `digital-downloads.json` 

### Example Output: Markdown

#### Digital Downloads

- **Product:** Test Strategy Template  
  **Price:** $5.99  
  **Link:** <WEB_FORM_URL>/test-strategy-template/

- **Product:** Bug Report Checklist  
  **Price:** $3.99  
  **Link:** <WEB_FORM_URL>/product/bug-report-checklist/

 
### Example Output: JSON
[
  {
    "name": "Test Strategy Template",
    "price": "$5.99",
    "url": "<WEB_FORM_URL>/product/test-strategy-template/"
  },
  {
    "name": "Bug Report Checklist",
    "price": "$3.99",
    "url": "<WEB_FORM_URL>/product/bug-report-checklist/"
  }
]

