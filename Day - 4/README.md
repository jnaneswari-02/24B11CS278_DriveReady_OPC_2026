
# AI Agents Workshop – Level 2
## Day 4: Tools, Structured Output and Google Sheets

### Project: Sweet Crumbs Home Bakery AI Assistant

## 1. Overview
This project demonstrates how to build an AI-powered bakery assistant using LangChain, Groq LLM, Python tools, Pydantic and Google Sheets.

The assistant can answer customer queries, check bakery prices and opening hours, validate cake orders and automatically save confirmed orders into a Google Spreadsheet.

## 2. Objectives
- Understand why AI agents need tools.
- Learn function calling using LangChain.
- Create Python tools using the `@tool` decorator.
- Build an AI agent using `create_agent`.
- Handle API rate limits and errors.
- Validate structured data using Pydantic.
- Connect Google Sheets using gspread.
- Automatically save customer orders.

## 3. Technologies Used
- Python
- Google Colab
- LangChain
- Groq API
- GPT-OSS-20B
- Pydantic
- Google Sheets
- gspread

## 4. Features

### 1. Get Price Tool
Checks the bakery menu and calculates the total price.

Menu:
- Plum Cake – ₹500
- Chocolate Cake – ₹650
- Cupcake – ₹80

### 2. Opening Hours Tool
Checks the bakery's opening hours for the requested day.

### 3. Order Management Tool
Collects customer details and saves confirmed orders into Google Sheets.

### 4. Pydantic Validation
Validates customer order details, including:
- Customer name
- Cake item
- Quantity
- Pickup date
- Eggless preference

### 5. AI Chat Assistant
Understands customer messages and decides which tool to call based on the request.

### 6. Google Sheets Integration
Automatically stores confirmed orders in a spreadsheet with the following columns:

`name | item | qty | date | eggless | total`

## 5. Project Workflow

1. Customer sends a message to the AI assistant.
2. The AI understands the customer's request.
3. The agent selects the required tool.
4. The tool checks prices or opening hours.
5. For orders, the assistant collects all required details.
6. Pydantic validates the order information.
7. The `log_order` tool calculates the total price.
8. The order is saved to Google Sheets.
9. The assistant confirms the order to the customer.

## 6. Installation and Setup

Install the required libraries:

```python
!pip install -q langchain langchain-groq gspread pydantic
```

### API Configuration

1. Create a Groq API key.
2. Open Google Colab Secrets.
3. Add a secret named `GROQ_API_KEY`.
4. Store your actual API key as its value.
5. Enable notebook access.
6. Authenticate your Google account for Sheets access.

Load the API key:

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

## 7. Execution

Run the notebook cells in the following order:

- Cell 1: Setup and Google Sheets Authentication
- Cell 2: Pydantic Order Model and Three Tools
- Cell 3: Create AI Agent and Chat Function
- Cell 4: View Agent Execution Trace

## 8. Testing

Test the assistant with the following customer messages:

| Customer Message | Expected Behaviour |
|---|---|
| Are you open on Sunday? | Displays opening hours |
| How much are 2 chocolate cakes? | Calculates ₹1,300 |
| I need 6 cupcakes | Calculates ₹480 |
| Do you have donuts? | Explains that donuts are unavailable |
| I want 2 plum cakes | Asks for missing customer details |
| I want 0 cupcakes | Rejects invalid quantity |

## 9. Expected Output

Example customer request:

"I'm Ravi. Please book 2 eggless chocolate cakes for 24 Dec."

Expected response:

"Saved: 2 x chocolate cake for Ravi on 24 Dec, Rs 1300."

The confirmed order is automatically added to the Google Sheet.

## 10. Learning Outcomes

After completing this task, I learned:

- How AI agents interact with external Python tools.
- How function calling works in LangChain.
- How to create descriptive and reusable tools.
- How to validate AI-generated data using Pydantic.
- How to integrate Google Sheets with Python.
- How to automate customer order management.
- How to inspect agent execution traces and handle errors.

## 11. Conclusion

The Sweet Crumbs Home Bakery AI Assistant demonstrates how an AI agent can move beyond simple conversations and perform real-world tasks.

By combining LangChain tools, Groq LLM, Pydantic validation and Google Sheets, the system automates price enquiries, opening-hours checks and customer order management while reducing manual work for the bakery owner.
