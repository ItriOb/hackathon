# BRD Processing System

Automated Business Requirements Document processing system using AWS Bedrock Claude Sonnet 4, LangChain, and Streamlit.

## Features

- 📄 **DOCX Parser**: Extracts structured content from BRD documents
- 🎯 **Epic Generation**: Creates epics with business value from requirements
- 📝 **User Story Generation**: Generates detailed user stories with acceptance criteria
- 🗂️ **Data Model Generation**: Creates Pydantic models from requirements
- 🧪 **Test Generation**: Generates pytest test cases for all user stories
- 🥒 **Gherkin Scenarios**: Creates BDD scenarios in Given-When-Then format
- 📊 **Export**: JSON, Excel, and traceability matrix exports

## Prerequisites

- Python 3.9+
- AWS Account with Bedrock access
- AWS credentials configured
- Claude Sonnet 4 model access in AWS Bedrock

## Installation

1. **Clone or download this repository**

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Configure AWS credentials:**

Create `~/.aws/credentials`:
```ini
[default]
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
```

Or set environment variables:
```bash
export AWS_ACCESS_KEY_ID=your_access_key
export AWS_SECRET_ACCESS_KEY=your_secret_key
export AWS_DEFAULT_REGION=us-east-1
```

4. **Ensure AWS Bedrock access:**
   - Request access to Claude Sonnet 4 in AWS Bedrock console
   - Model ID: `anthropic.claude-sonnet-4-20250514`

## Usage

### Run the Streamlit App

```bash
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

### Using the Application

1. **Initialize AWS Bedrock**
   - Select your AWS region in the sidebar
   - Click "Initialize AWS Bedrock" button
   - Wait for connection confirmation

2. **Upload BRD Document**
   - Click "Browse files" or drag & drop a .docx file
   - Preview the document sections

3. **Configure Processing Options**
   - Select which artifacts to generate (Epics, Models, Tests, Gherkin)

4. **Process Document**
   - Click "🚀 Process Document"
   - Monitor progress bar
   - View results in tabs

5. **Export Results**
   - Download JSON for programmatic use
   - Download Excel for stakeholder review
   - Download traceability matrix for requirements tracking

## Architecture

```
app.py
├── Pydantic Models (Epic, UserStory, DataModel, TestCase, GherkinScenario)
├── DOCXParser (Document extraction)
├── BedrockClient (AWS Bedrock integration)
├── PromptTemplates (LLM prompts)
├── BRDPipeline (Processing orchestration)
├── Exporters (JSON, Excel, CSV)
└── Streamlit UI (Web interface)
```

## Key Components

### Document Parsing
- Extracts sections by heading structure
- Preserves document organization
- Handles tables and formatted content

### LLM Processing
- Uses Claude Sonnet 4 via AWS Bedrock
- Structured output with Pydantic models
- Template-based prompt engineering

### Pipeline Workflow
1. Parse DOCX → Extract sections
2. Generate Epics → From requirements
3. Generate User Stories → From epics
4. Generate Data Models → From entities
5. Generate Tests → From user stories
6. Generate Gherkin → From acceptance criteria

### Export Formats
- **JSON**: Complete structured data
- **Excel**: Multiple sheets (Epics, Stories, Models, Tests, Gherkin)
- **CSV**: Traceability matrix

## Customization

### Modify Prompt Templates
Edit the `PromptTemplates` class in `app.py`:
```python
class PromptTemplates:
    EPIC_GENERATION = """Your custom prompt..."""
    USER_STORY_EXPANSION = """Your custom prompt..."""
    # etc.
```

### Adjust Model Parameters
Edit the `BedrockClient` initialization:
```python
self.client = ChatBedrock(
    model_id=self.model_id,
    region_name=self.region_name,
    model_kwargs={
        "temperature": 0.3,  # Adjust for creativity
        "top_p": 0.9,
        "max_tokens": 4096
    }
)
```

### Add New Artifact Types
1. Create a new Pydantic model
2. Add prompt template
3. Add generation method to `BRDPipeline`
4. Add UI tab in Streamlit

## Troubleshooting

### AWS Connection Issues
- Verify AWS credentials are configured correctly
- Check IAM permissions for Bedrock access
- Ensure Claude Sonnet 4 is available in your region

### Document Parsing Issues
- Ensure DOCX file is properly formatted
- Use heading styles (Heading 1, Heading 2, etc.)
- Check for document corruption

### Generation Quality Issues
- Adjust temperature parameter (lower = more focused)
- Modify prompt templates for better instructions
- Ensure BRD sections are clearly structured

### Performance Issues
- Large documents may take 5-10 minutes to process
- Consider processing in batches
- Use progress callbacks to monitor status

## Logging

Logs are written to console with timestamps:
```
2024-01-15 10:30:45 - __main__ - INFO - Extracted 5 sections from document
2024-01-15 10:31:12 - __main__ - INFO - Generated 3 epics from section: Functional Requirements
```

## Cost Considerations

- AWS Bedrock charges per token
- Claude Sonnet 4 pricing: ~$3 per million input tokens, ~$15 per million output tokens
- Average BRD processing: ~50K-200K tokens
- Estimated cost per document: $0.50-$2.00

## Security Notes

- AWS credentials should never be committed to version control
- Use IAM roles when running on EC2/ECS
- Sensitive BRD content is sent to AWS Bedrock (review compliance requirements)
- Generated artifacts may contain confidential information

## Limitations

- Requires well-structured DOCX documents
- JSON extraction from LLM responses is heuristic-based
- Large documents (>50 pages) may timeout
- Quality depends on BRD clarity and detail

## Future Enhancements

- [ ] Add support for PDF input
- [ ] Implement RAG for referencing past BRDs
- [ ] Add custom field extraction rules
- [ ] Support for Jira integration
- [ ] Real-time collaboration features
- [ ] Version control for generated artifacts

## License

MIT License - feel free to modify and use for your projects

## Support

For issues or questions:
1. Check logs for error messages
2. Verify AWS Bedrock connectivity
3. Review prompt templates for accuracy
4. Test with a simple BRD first

## Contributing

Contributions welcome! Areas for improvement:
- Better JSON parsing from LLM responses
- Additional export formats
- Integration with project management tools
- Enhanced error handling
- Performance optimizations
