

# 🧠 AI-Powered Doctor Appointment System Using LangChain and LangGraph

## 🎥 Overview

This project demonstrates an **end-to-end implementation** of a multi-agent AI system for booking doctor appointments. It integrates:

- **LangGraph** – Workflow automation & agent routing
- **LangChain** – Tool & agent integration
- **FastAPI** – Backend API endpoints
- **Streamlit** – Frontend user interface
- **Pandas & CSV** – Data storage & access
- **Pydantic** – Data validation

---

## 📌 Problem Statement

Build a **multi-agent AI-powered doctor appointment system** capable of:

- Handling doctor **availability**, **specialization**, **booking**, **cancellation**, and **rescheduling**
- Using **supervisor architecture** to delegate tasks to multiple agents
- Providing a **realistic medical assistant experience**

---

## 🧠 Architecture

A **Supervisor Multi-Agent System** using LangGraph:

- **Supervisor Agent**: Delegates tasks based on user input
- **Information Agent**: Handles queries like doctor availability
- **Booking Agent**: Handles appointment management
- **Finish Node**: Terminates flow for invalid/irrelevant queries

---

## 🧰 Tech Stack

| Component      | Technology       |
|----------------|------------------|
| Agents & Flow  | LangGraph        |
| Prompt & Tools | LangChain        |
| Backend API    | FastAPI          |
| Frontend UI    | Streamlit        |
| Data Handling  | Pandas, CSV      |
| Validation     | Pydantic         |
| Python Version | >= 3.9           |

---

## 🗂️ Folder Structure

```plaintext
doctor_appointment_multi_agent/
├── data/                  # Doctor availability data (CSV)
├── data_models/           # Pydantic validation models
├── notebooks/             # Jupyter/IPYNB experiments
├── prompt_library/        # Prompt configuration
├── toolkit/               # LangChain tools
├── utils/                 # Utility files (e.g. LLM loader)
├── agents.py              # Agent definitions & LangGraph workflow
├── main.py                # FastAPI endpoints
├── streamlit_ui.py        # Streamlit UI frontend
├── requirements.txt       # Required packages
├── setup.py               # Local package installation
├── .gitignore             # Git ignore config
````

---

## 📋 Dataset Description

Stored as `doctor_availability.csv` with 4000+ rows. Columns:

* `date_slot` – Date and time
* `specialization`
* `doctor_name`
* `is_available` – Boolean
* `patient_to_attend` – Patient ID or `None` if free

---

## 📦 Pydantic Models

| Model                       | Purpose                             |
| --------------------------- | ----------------------------------- |
| `DateTimeModel`             | Validates `dd-mm-yyyy HH:MM` format |
| `DateModel`                 | Validates only date portion         |
| `IdentificationNumberModel` | Ensures patient ID is 7–8 digits    |

---

## 🛠️ LangChain Tools

Defined inside `toolkit/toolkits.py`. Tools include:

1. `check_availability_by_doctor(date, doctor)`
2. `check_availability_by_specialization(date, spec)`
3. `set_appointment(date_time, id, doctor)`
4. `cancel_appointment(date_time, id, doctor)`
5. `reschedule_appointment(date_time, id, doctor)`

---

## 💬 Prompt Engineering

Defined in `prompt_library/prompts.py`:

* **System Prompt** includes:

  * Agent descriptions (Information, Booking, Finish)
  * Task delegation instructions
  * Behavioral constraints

---

## 🧠 Agent Design (`agents.py`)

* Class: `DoctorAppointmentAgent`
* Agents: `supervisor_node`, `information_node`, `booking_node`
* Uses `StateGraph` (LangGraph) with:

  * `state` containing `message`, `query`, `reasoning`, etc.
  * Edges/routes determined dynamically using `CommandRouter`

---

## ⚙️ LLM Setup (`utils/llm.py`)

* Loads OpenAI model via API key stored in `.env`
* LLM class returns initialized model
* Tested interactively via notebook

---

## 🌐 Backend API (`main.py`)

* Built with **FastAPI**
* Endpoint: `/execute`
* Accepts: `UserQuery` with `message` and `ID`
* Invokes LangGraph workflow and returns result
* Optional: SSL handling for secure deployment

---

## 🎨 Frontend UI (`streamlit_ui.py`)

* User inputs: `User ID`, `Query`
* Calls FastAPI backend
* Displays response JSON in a readable form
* Modular and extendable into chatbot format

---

## ✅ Execution Flow

1. **Create Environment**:
   `conda create --name penv python=3.9`

2. **Activate Environment**:
   `source activate ./penv`

3. **Install Requirements**:
   `pip install -r requirements.txt`

4. **Run FastAPI Server**:

   ```bash
   uvicorn main:app --reload --port 8002
   ```

5. **Run Streamlit UI**:

   ```bash
   streamlit run streamlit_ui.py
   ```

6. **Access Swagger Docs**:
   Visit: `http://127.0.0.1:8002/docs`

---

## 🧪 Notebook Demonstration

The IPython notebook demonstrates:

* Input validation for date, ID

* Tool testing (availability check, booking, cancellation)

* Workflow invocation using sample queries

* Example:

  ```json
  {
    "message": "Check if a general dentist is available on 8th August 2024 at 8:00 PM",
    "ID": "1234567"
  }
  ```

* Output includes:

  * Time slots
  * Booking confirmation
  * Intelligent reasoning (via GPT-4)

---

## 📎 Resources

* 📂 GitHub Repo (Code & Requirements)
* 📒 IPython Notebook included
* 🔑 `.env` file with API keys (only OpenAI used here)



This LangGraph-based multi-agent system serves as a real-world **agentic AI project**. It demonstrates:

* Modular development
* Effective use of LangChain tools
* Workflow orchestration with LangGraph
* Deployable architecture (API + UI)




```
conda create -p venv python=3.10 -y
```

```
conda activate ./venv
```

```
pip install -r requirements.txt
```