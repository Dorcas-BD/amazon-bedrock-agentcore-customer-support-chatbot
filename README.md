# Customer Support Chatbot with Amazon Bedrock AgentCore

A customer support chatbot for a fictional online shop. It uses prompt engineering to route customer requests, answer FAQ questions, collect bug reports, and direct unsupported requests to human support.

## Features

- Collects a bug description, reproduction steps, and environment before creating a ticket.
- Answers supported questions using the shop FAQ.
- Hands off uncovered questions and out-of-scope requests to human support.
- Asks clarifying questions when bug reports lack required details.
- Includes instructions to resist prompt-injection attempts.
- Generates a JSONL dataset for Amazon Bedrock Evaluations.

## Architecture

- Amazon Bedrock AgentCore managed harness
- Amazon Bedrock AgentCore Gateway
- AWS Lambda for bug-report processing
- Amazon DynamoDB for ticket storage
- Amazon Nova Pro
- Python and AWS CloudFormation

## Project Files

- `system_prompt.txt`: chatbot instructions and routing rules
- `online_shop_faq.md`: FAQ source material
- `create_bug_report.py`: bug-report tool
- `cloudformation-tool.yaml`: tool infrastructure
- `cloudformation-testing.yaml`: evaluation infrastructure
- `setup_gateway.py`: gateway setup
- `create_harness.py`: harness creation and updates
- `chat.py`: interactive chat client
- `harness-tests.json`: seven test scenarios
- `generate-eval-dataset.py`: evaluation dataset generator
- `output_eval_dataset.jsonl`: generated evaluation dataset
- `submission_evidence/`: saved test transcripts and supporting evidence

## Testing

Seven scenarios cover bug reporting, FAQ questions, uncovered questions, out-of-scope requests, ambiguous reports, and prompt injection.

All seven scenarios previously ran successfully, and the evaluation dataset was generated. Manual testing also confirmed that a bug report was stored in DynamoDB and returned a ticket ID.

**Evaluation limitation:** The Amazon Bedrock Evaluation jobs reported zero successfully evaluated sessions. No evaluation score is claimed.

## Running Locally

Install dependencies:

    pip install -r requirements.txt

Generate the evaluation dataset:

    python generate-eval-dataset.py --tests-json harness-tests.json

Running the application requires suitable AWS credentials, permissions, and AWS resources.

## Security

Never commit AWS credentials, access keys, secret tokens, or local credential files. Review AWS resource identifiers before making configuration files public.

## Technologies

Python, Amazon Bedrock AgentCore, Amazon Nova Pro, AWS Lambda, Amazon DynamoDB, AWS CloudFormation, JSONL
