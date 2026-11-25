# AI Agents Workshop – Day 3

## Your First AI Agent: LangChain

### Overview

Day 3 of the AI Agents Workshop focuses on understanding AI Agents and learning how to build AI-powered applications using **LangChain and Groq API**.

In this session, I explored the difference between chatbots and AI agents, learned the basic architecture of an agent, understood the agent loop, and rebuilt the Sweet Crumbs Home Bakery Assistant using LangChain.

The practical work was completed using Google Colab and Python.

## Technologies Used

- Python
- Google Colab
- Groq API
- LangChain
- LangChain-Groq
- CSV
- JSON

## Topics Covered

### 1. Chatbot vs AI Agent

- Understood the difference between a chatbot and an AI agent.
- A chatbot provides answers, whereas an agent can perform actions using tools to achieve a goal.
- Learned how tools make an AI application more useful.

### 2. Four Components of an AI Agent

Learned the four main components:

- **Brain:** Large Language Model (LLM) that understands and makes decisions.
- **Instructions:** System prompt that defines the agent's role and rules.
- **Tools:** Functions that allow the agent to perform tasks.
- **Memory:** Stores conversation history and useful information.

### 3. Agent Loop

Understood how an AI agent works through the following steps:

**Think → Act → Observe → Repeat**

- Think about the user's request.
- Act by selecting and calling a tool.
- Observe the tool's result.
- Repeat until the task is completed.

### 4. Three Levels of AI

Explored three levels of AI:

| Level | Description |
|---|---|
| Traditional AI | Follows predefined rules |
| Generative AI | Generates text, images, or other content |
| Agentic AI | Uses tools and makes decisions to complete tasks |

### 5. Choosing the Right AI Approach

Learned when to use:

- **Plain Python code:** For fixed calculations and predefined operations.
- **One LLM call:** For generating content, answering questions, and translation.
- **AI Agent:** For tasks requiring decisions, multiple steps, and tool usage.

### 6. Introduction to LangChain

Learned how LangChain simplifies the development of LLM applications.

- Installed LangChain and LangChain-Groq.
- Connected the Groq model using `ChatGroq`.
- Used `invoke()` to send messages to the model.
- Understood how LangChain provides a common interface for different language models.

### 7. LangChain Basics

Practiced three important components:

- **Chat Model:** Generates responses using an LLM.
- **Prompt Template:** Creates reusable prompts with placeholders.
- **Chain:** Connects multiple components using the pipe (`|`) operator.

Example:

```python
chain = prompt | llm | StrOutputParser()
```

### 8. Conversation Memory

- Used `MessagesPlaceholder` to include conversation history.
- Maintained previous messages using a Python list.
- Created an `ask()` function to manage conversations.
- Tested whether the assistant could remember customer information.

### 9. Testing the Assistant

Created a `tests.csv` file containing customer questions and expected keywords.

Implemented automated testing using Python and CSV.

The testing process included:

- Reading test cases.
- Sending questions to the assistant.
- Checking whether expected keywords appeared.
- Displaying PASS or FAIL results.
- Calculating the overall pass percentage.

## Practical Project: Sweet Crumbs Home Bakery Assistant

Rebuilt the bakery customer support assistant using LangChain.

### Sample Menu

| Product | Price |
|---|---:|
| Plum Cake | ₹500 |
| Chocolate Cake | ₹650 |
| Cupcake | ₹80 |

### Features

- Answers customer questions.
- Provides bakery menu information.
- Responds to eggless cake queries.
- Follows the 24-hour advance-order rule.
- Maintains conversation history.
- Uses prompt templates and LangChain chains.
- Tests responses using automated test cases.

## Learning Outcomes

After completing Day 3, I learned how to:

- Understand the fundamentals of AI agents.
- Differentiate chatbots, generative AI, and agentic AI.
- Understand the four components of an AI agent.
- Explain the Think–Act–Observe–Repeat loop.
- Connect Groq with LangChain.
- Create reusable prompt templates.
- Build LangChain chains using the pipe operator.
- Maintain conversation history.
- Create automated test cases and calculate pass rates.
- Understand the basics of creating an AI agent.

## Security Notes

- API keys are stored using Google Colab Secrets.
- API keys should never be exposed in public repositories.
- Avoid hardcoding sensitive credentials in notebook files.

## Future Improvements

- Add real Python functions as agent tools.
- Enable the agent to calculate prices automatically.
- Add order booking and order tracking.
- Improve memory management.
- Add more customer test cases.
- Build a complete tool-using AI agent.

## Conclusion

Day 3 helped me understand the fundamentals of AI agents and how LangChain simplifies building LLM-powered applications. I also rebuilt the Sweet Crumbs Home Bakery Assistant, implemented conversation memory, and tested its responses using CSV-based test cases.

This session provided the foundation for developing tool-using AI agents in the upcoming sessions.

---

**Workshop:** AI Agents Workshop – Level 2  
**Day:** 3  
**Project:** Sweet Crumbs Home Bakery Assistant  
**Environment:** Google Colab  
**Programming Language:** Python  
**LLM Provider:** Groq  
**Framework:** LangChain
