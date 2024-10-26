Application 1: Rule Engine with AST
Zeotap | Software Engineer Intern | Assignment | Application 1

Table of Contents
Introduction
Technical Details
Setup Instructions
Execution Guide
Solution Details
Solution Summary
Code Layout
Additional Insights
Approach
Reflection
Conclusion
Introduction
I reviewed the assignment description multiple times to ensure that I fully understood all requirements.

My code might feel a bit like a narrative, so I’ve kept this README concise and structured:

The code is thoroughly commented, with documentation written to align with Doxygen for React code and Sphinx for Python code.
Unittests cover various scenarios, including edge cases, with both positive and negative test cases, achieving over 80% coverage.
This README focuses on technical aspects first, followed by the solution's description. It concludes with insights on my approach and design decisions.
Technical Details
Setup Instructions
To keep the solution platform-agnostic, I’ve packaged it using Docker. However, you can also follow these steps to run it locally without Docker.

Frontend

bash
Copy code
cd frontend/
npm install
Backend

If poetry is not already installed, set it up as follows:

bash
Copy code
python3 -m venv $VENV_PATH
$VENV_PATH/bin/pip install -U pip setuptools
$VENV_PATH/bin/pip install poetry
Then, create a virtual environment and install dependencies:

bash
Copy code
cd backend/
poetry install
Database

After completing poetry install, run the following command to initialize raw data in PostgreSQL. Ensure the connection credentials are specified in .env:

bash
Copy code
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
Execution Guide
Assuming the above setup steps were successful:

Frontend
bash
Copy code
npm run dev
Backend
bash
Copy code
poetry run python main.py --dev
Database
bash
Copy code
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
Solution Details
The solution consists of a UI, an API, and a database, as outlined in the documentation. For the UI, I chose Next.js for familiarity. The API is built with FastAPI to prioritize both runtime efficiency and developer productivity.

Solution Summary
Here’s a brief overview:

The UI communicates with the REST API and displays the AST using react-d3-tree.
The backend parses raw input strings through tokenization via tokenizer(). A custom regex helps in identifying lexemes. Parsed tokens are then processed by a Parser object, resulting in an AST node.
The AST is serialized into JSON and saved in the database. There are potential optimizations for storage, like using hash-based key-value storage for nodes. This setup allows for tree traversal, change tracking, and optimized storage. Similar to Dropbox's file storage model, this can save space while maintaining data isolation.
Code Layout
Below is the file structure and their descriptions:

Backend
File Description
main.py Server entry point
poetry.lock Dependency file managed by Poetry
pyproject.toml Python project metadata
rule_engine/ast_utils.py Contains AST-related classes and utilities, like Node
rule_engine/database.py Database ORM and read/write utilities
rule_engine/main.py API entry point and contracts
rule_engine/models.py Database schema
rule_engine/parser_utils.py Parser and tokenizer utilities
Frontend
File Description
app/ Application source code
app/components/ASTTree.tsx AST visualization component
app/services/api.ts Middleware to connect to REST API
app/page.tsx Main UI entry point
Design Discussion
Below is the low-level class design:

java
Copy code
// Core Classes and Methods for AST and Operators
Class Node:
// Attributes and methods representing node and operator handling.

Class Operator:
// Methods for operator handling and logical evaluation.

Class Condition<T>:
// Attributes and methods to handle condition evaluation based on type.

Class AST:
// AST root node and methods to evaluate rules, create rules, and combine rules.
For parser and tokenizer functions:

java
Copy code
// Parser and Tokenizer logic to handle expression parsing and AST generation.
Function tokenize(rule: String) -> List<String]:
// Returns tokens from a given rule.
Class Parser:
// Attributes and methods to parse and construct AST nodes.
Additional Insights
This section shares more about the approach and thought process.

Approach
My approach involved the following steps:

Initially, I thoroughly reviewed the assignment to understand its requirements.
I researched operator heuristics, which were key to my design.
Using my prior experience with lex and bison in compiler coursework, I mapped out the AST structure and relationships.
I implemented the parser, then focused on tree traversal to enable creation, evaluation, and storage.
After coding, everything fell into place and became straightforward.
Reflection
This assignment was well-rounded, combining compiler concepts, algorithmic thinking, and software engineering principles. It was both challenging and enjoyable, and I gained a lot from working on the heuristics involved. Thank you for this learning opportunity.

Conclusion
Thank you for reviewing my submission!
