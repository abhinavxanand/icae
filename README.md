## Initial Setup and Configuration

- The code starts by loading environment variables using dotenv
- Configures Azure OpenAI API credentials (key, version, base URL, deployment name)
- Sets up the Azure OpenAI client for making API calls
- Defines validation tools that will help check and format different types of data


# Document Processing

- Takes a PDF file (sample_contract.pdf) as input
- Uses DocumentConverter to convert the PDF into markdown format
- This makes the contract text easier to process


# Information Extraction (First Phase)

- Use one of the two prompts (PROMPT and PROMPT1) to guide the extraction
- PROMPT is concise and focuses on key fields
- PROMPT1 is more detailed with specific instructions for handling missing data
- ## Makes an API call to Azure OpenAI to extract information like:

- Contract ID
- Contract Name
- Status
- Currency
- Customer details
- Dates
- Payment terms
- Contract amount
- Metadata




# Initial Output Processing

- Takes the extracted information and formats it
- Uses pretty printing for markdown content
- Converts the response into JSON format
- Pretty prints the JSON for readability


# Validation Process (Tool-based Validation)

- Goes through each extracted field
- For each field, uses specific validation tools based on field type:

- Dates are checked for correct format (YYYY-MM-DD)
- Monetary values are checked for proper number format
- Status fields are checked against valid options
- IDs are checked for presence and format


- Creates a validation log recording any issues found
- Handles metadata fields separately with their own validation


# LLM-based Validation and Correction

- Takes the validation results and logs
- Uses a specific prompt (VALID_PROMPT) to guide the correction process
## The prompt includes rules for:

- Date formatting
- Monetary value standardization
- Handling missing fields
- Metadata validation
- Makes another API call to Azure OpenAI to get corrected data


# Final Processing

- Extracts the corrected JSON from the LLM response
- Formats and validates the final data
- Prepares the data for API submission


# API Submission

- Prepares a payload with the corrected and validated data
- Includes all required fields for the Zenskar API
- Makes a POST request to the API
- Handles the API response:



Installation
1. Clone the repository:
```
git clone https://github.com/abhinavxanand/assignment.git

```
2. Create and activate virtual environment:

```
python -m venv venv
```
For Linux:
```
source venv/bin/activate
```
For Windows:
```
source venv\Scripts\activate

```
3. Install Requirements:
```
pip install -r requirements.txt

```
4. Run
```
python main.py

```

