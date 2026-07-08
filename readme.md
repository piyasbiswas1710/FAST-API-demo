# Patient Management System API

A simple REST API built with **FastAPI** to manage patient health records —
including automatic BMI calculation and health verdict classification
(Underweight / Normal / Overweight / Obese).

Patient data is stored in a local `patients.json` file (no external database
required), making this a lightweight project for learning FastAPI, Pydantic
models, and RESTful API design.

---

## 🛠️ Tech Stack

- **Python 3.14**
- **FastAPI** — web framework
- **Uvicorn** — ASGI server
- **Pydantic** — data validation and serialization

---

## 📁 Project Structure

```
fast-API/
├── main.py            # All API routes and Pydantic models
├── patients.json       # Patient data storage (JSON file as a mock DB)
├── requirements.txt     # Python dependencies
└── .gitignore
```

---

## ⚙️ Setup & Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/piyasbiswas1710/FAST-API-demo.git
   cd FAST-API-demo
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv myvenv

   # Windows
   myvenv\Scripts\activate

   # Mac/Linux
   source myvenv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the server**
   ```bash
   uvicorn main:app --reload
   ```

5. **Open the interactive API docs**
   ```
   http://127.0.0.1:8000/docs
   ```

---

## 📌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Welcome message |
| `GET` | `/about` | API description |
| `GET` | `/view` | View all patient records |
| `GET` | `/patient/{patient_id}` | View a specific patient by ID |
| `GET` | `/sort?sort_by=&order=` | View patients sorted by a field (e.g. `bmi`, `age`) |
| `POST` | `/create` | Add a new patient record |
| `PUT` | `/edit/{patient_id}` | Update an existing patient's details |
| `DELETE` | `/delete/{patient_id}` | Remove a patient record |

---

## 🧮 Computed Fields

Every patient record automatically includes two calculated fields —
these are **not** provided by the user, they're derived from `height` and `weight`:

| Field | Formula | Description |
|---|---|---|
| `bmi` | `weight / (height ** 2)` | Body Mass Index, rounded to 2 decimals |
| `verdict` | Based on `bmi` | `Underweight` / `Normal` / `Overweight` / `Obese` |

---

## 📥 Example — Create a Patient

**Request**
```http
POST /create
Content-Type: application/json

{
  "id": "P006",
  "name": "Test Patient",
  "city": "Delhi",
  "age": 30,
  "gender": "male",
  "height": 1.75,
  "weight": 80
}
```

**Response**
```json
{
  "message": "patient created successfully"
}
```

---

## 📤 Example — View a Patient

**Request**
```
GET /patient/P006
```

**Response**
```json
{
  "name": "Test Patient",
  "city": "Delhi",
  "age": 30,
  "gender": "male",
  "height": 1.75,
  "weight": 80,
  "bmi": 26.12,
  "verdict": "Normal"
}
```

---

## 🚧 Notes / Future Improvements

- Currently uses a JSON file as storage — could be migrated to a proper
  database (SQLite/PostgreSQL) for production use.
- No authentication/authorization implemented yet.
- Consider adding pagination for the `/view` endpoint as data grows.

---

## 👤 Author

**Piyas Biswas**
[GitHub](https://github.com/piyasbiswas1710)