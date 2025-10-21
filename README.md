<h1 align="center">🧠 mcqgene</h1> <p align="center">AI-Powered Multiple-Choice Question (MCQ) Generator — Automate quiz creation with OpenAI</p> <p align="center"> <img src="https://img.shields.io/badge/Python-3.11-blue?logo=python"> <img src="https://img.shields.io/badge/OpenAI-GPT-3.5-Turbo-black?logo=openai"> <img src="https://img.shields.io/badge/License-MIT-yellow.svg"> </p>

🎯 A smart tool that converts educational or textual content into Multiple-Choice Questions (MCQs) using OpenAI GPT-3.5 Turbo.
Ideal for educators, e-learning platforms, and AI-driven quiz systems.

🚀 Features

1. Automatically generates MCQs from any given text

2. Returns both questions and correct answers

3.  Adjustable question count and difficulty level

4. Clean JSON output for programmatic integration

5. Modular code design (import as a library or use via CLI)

 Ready for API deployment or educational integration
----


⚙️ Setup
1. Clone the repository
git clone https://github.com/obinnachike/mcqgene.git
cd mcqgene

2. Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

3. Install dependencies
pip install -r requirements.txt

4. Add your OpenAI API key

Create a .env file in the root directory:

OPENAI_API_KEY=your_openai_api_key_here


 Never commit your .env file — ensure it’s in .gitignore.

 How It Works

Input Text — The app reads educational or text content (e.g., lecture notes, articles).

Prompt Engineering — A structured OpenAI prompt is built to request MCQs with answers.

Model Generation — GPT-3.5 Turbo processes the content and produces formatted MCQs.

Output Formatting — Questions, choices, and answers are returned in JSON for easy parsing.

Integration — The tool can be imported as a module, used from CLI, or exposed via an API.

 Example (Python Usage)
from mcqgene.generator import MCQGenerator

generator = MCQGenerator(api_key="YOUR_OPENAI_API_KEY")

content = """
Artificial Intelligence is the simulation of human intelligence processes by machines, especially computer systems.
"""

questions = generator.generate_mcqs(content, num_questions=3)

for q in questions["questions"]:
    print(f"Q: {q['question']}")
    for opt in q["options"]:
        print(opt)
    print(f"Answer: {q['answer']}\n")


Output Example:

Q: What does AI primarily simulate?
a) Human intelligence
b) Machine automation
c) Natural systems
d) Weather patterns
Answer: a) Human intelligence

 CLI Usage

You can also generate questions directly from the terminal:

python test.py --file sample.txt --num 5


Arguments:

--file: Path to the text file

--num: Number of questions to generate

--output: (optional) Output file for JSON results

Example:

python test.py --file biology.txt --num 10 --output mcqs.json

 API Integration

A simple REST API can be deployed using Flask or FastAPI.

Example api/MCQGENERATOR.py (FastAPI):
from fastapi import FastAPI, Body
from mcqgene.generator import MCQGenerator

app = FastAPI()
generator = MCQGenerator()

@app.post("/generate")
def generate_mcqs_endpoint(content: str = Body(...), num_questions: int = 5):
    return generator.generate_mcqs(content, num_questions)

Run the API
uvicorn api.main:app --reload


Then test with:

curl -X POST http://127.0.0.1:8000/generate \
     -H "Content-Type: application/json" \
     -d '{"content": "Photosynthesis is a process...", "num_questions": 5}'

 Deployment

You can deploy mcqgene easily on:

Render — Python web service

Railway.app — easy Flask/FastAPI hosting

Heroku — for quick PaaS setup

Docker — containerize for production

Example Dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "api/main.py"]


Then build and run:

docker build -t mcqgene .
docker run -p 8080:8080 mcqgene

 Requirements

Python 3.9 or higher

openai

python-dotenv

(Optional) Flask or FastAPI for API integration


 Acknowledgements

OpenAI
 — GPT-3.5 Turbo API

FastAPI
 / Flask
 — for API deployment

Shields.io
 — for badges

Uvicorn
 — for ASGI serving

🖋 Author: Obinna Chike
