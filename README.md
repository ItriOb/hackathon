# hackathon
# Create a complete backend system for BRD processing using Streamlit, LangChain, AWS Bedrock Claude Sonnet 4, and python-docx:
# 
# Requirements:
# 1. DOCX Parser: Read .docx BRD file, extract text by sections (headings), preserve structure, handle tables
# 2. AWS Bedrock Integration: Use langchain-aws ChatBedrock with model "anthropic.claude-sonnet-4-20250514"
# 3. Prompt Templates: Create templates for generating epics, user stories, data models (Pydantic), functional tests (pytest), and Gherkin scenarios
# 4. Output Parsers: Use Pydantic models for structured outputs - Epic, UserStory, DataModel, TestCase, GherkinScenario
# 5. Processing Pipeline: Sequential chain that takes BRD sections → generates epics → user stories → data models → tests
# 6. Export Functions: JSON and Excel export for all generated artifacts
# 7. Error Handling: Try-catch blocks, logging, validation
# 8. Caching: Session state management for parsed documents and generated outputs
#
# File structure:
# - backend/document_parser.py: DOCX parsing with python-docx, section extraction
# - backend/bedrock_client.py: AWS Bedrock client setup, LangChain integration
# - backend/prompt_templates.py: All prompt templates for different generation tasks
# - backend/models.py: Pydantic models for Epic, UserStory, DataModel, TestCase, GherkinScenario
# - backend/pipeline.py: Main processing pipeline orchestrating all steps
# - backend/exporters.py: JSON and Excel export utilities
# - backend/utils.py: Helper functions, validators
#
# Include type hints, docstrings, error handling, and logging throughout



# Generate complete Python backend with these exact specifications:
#
# backend/models.py:
# - Pydantic models: Epic (title, description, business_value, priority, user_stories[])
# - UserStory (id, title, description, role, action, benefit, acceptance_criteria[], epic_id)
# - DataModel (entity_name, fields[], relationships[], pydantic_code)
# - TestCase (test_name, test_type, description, test_code, user_story_id)
# - GherkinScenario (feature, scenario, given[], when[], then[], user_story_id)
#
# backend/document_parser.py:
# - parse_docx(file_path) -> Dict[str, str]: Extract sections by heading styles
# - extract_tables(file_path) -> List[Dict]: Parse DOCX tables
# - identify_section_type(section_text) -> str: Classify section as requirements/objectives/constraints
#
# backend/bedrock_client.py:
# - BedrockClient class with ChatBedrock initialization
# - generate_completion(prompt, system_prompt, response_model) -> Pydantic object
# - stream_completion for long responses
# - Error handling with exponential backoff retry
#
# backend/prompt_templates.py:
# - EPIC_GENERATION_TEMPLATE: LangChain PromptTemplate with variables {brd_section}
# - USER_STORY_TEMPLATE: Generate stories from epic with {epic_description}
# - DATA_MODEL_TEMPLATE: Extract entities from {requirements_text}
# - PYTEST_TEMPLATE: Generate tests from {user_story}
# - GHERKIN_TEMPLATE: Convert {acceptance_criteria} to scenarios
#
# backend/pipeline.py:
# - BRDPipeline class: orchestrate full workflow
# - process_document(docx_path) -> Dict with all artifacts
# - Methods: generate_epics(), generate_stories(), generate_models(), generate_tests()
# - Progress callbacks for Streamlit integration
#
# backend/exporters.py:
# - export_to_json(artifacts, output_path)
# - export_to_excel(artifacts, output_path): Multiple sheets for epics/stories/tests
# - generate_traceability_matrix(): Link requirements to stories to tests
#


# Step 1: Generate just the models.py file with all Pydantic models for Epic, UserStory, DataModel, TestCase, GherkinScenario with validation

# Step 2: Generate document_parser.py with DOCX parsing using python-docx, section extraction by heading styles, table parsing

# Step 3: Generate bedrock_client.py with LangChain ChatBedrock setup for Claude Sonnet 4, structured output with Pydantic, retry logic
# Use boto3 for AWS credentials, python-docx for parsing, langchain-aws for Bedrock, openpyxl for Excel
# Add comprehensive logging with Python logging module
# Include unit test examples with pytest
