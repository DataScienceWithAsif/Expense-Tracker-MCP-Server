# 💸 Expense Tracker MCP Server

<div align="center">

A lightweight, production-ready **Model Context Protocol (MCP) server** for tracking expenses, listing transactions, and generating summaries.

![Python](https://img.shields.io/badge/Python-3.14+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastMCP](https://img.shields.io/badge/FastMCP-Enabled-111827?style=for-the-badge)
![SQLite](https://img.shields.io/badge/SQLite-Local%20DB-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

</div>

---

## ✨ Features

- ✅ Add expense entries with date, amount, category, subcategory, and note
- ✅ List expenses in a date range
- ✅ Summarize spending by category (with optional category filtering)
- ✅ Expose categories as an MCP resource
- ✅ Uses async DB operations (`aiosqlite`) for better concurrency
- ✅ Auto-initializes SQLite schema on startup

---

## 🧱 Tech Stack

- **Server Framework:** `fastmcp`
- **Database:** SQLite (`expenses.db` in system temp directory)
- **Async DB Layer:** `aiosqlite`
- **Language:** Python 3.14+

---

## 📂 Project Structure

```text
Expense-Tracker-MCP-Server/
├── main.py            # MCP server, tools, DB initialization, resource exposure
├── categories.json    # Category/subcategory definitions
├── requirements.txt   # pip dependencies
├── pyproject.toml     # project metadata/dependencies
├── uv.lock            # lockfile for uv workflows
└── README.md
```

---

## ⚙️ Setup

### 1) Clone and enter project

```bash
git clone <your-fork-or-repo-url>
cd Expense-Tracker-MCP-Server
```

### 2) Create virtual environment

```bash
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
# .venv\Scripts\activate   # Windows
```

### 3) Install dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Run the Server

```bash
python main.py
```

Server starts on:

- **Host:** `0.0.0.0`
- **Port:** `8000`
- **Transport:** `http`

---

## 🛠️ MCP Tools

### `add_expense(date, amount, category, subcategory="", note="")`
Add a new expense record.

### `list_expenses(start_date, end_date)`
Return expenses between two dates (inclusive), newest first.

### `summarize(start_date, end_date, category=None)`
Return grouped totals and counts by category for a date range.

---

## 📦 MCP Resource

### `expense:///categories`
Returns available categories as JSON.

- Reads from `categories.json`
- Falls back to built-in default categories if file is missing

---

## 🗃️ Database Details

- SQLite database path is set dynamically to system temp directory:
  - `TEMP_DIR/expenses.db`
- Table: `expenses`

| Column      | Type    | Notes |
|-------------|---------|-------|
| id          | INTEGER | Primary key, autoincrement |
| date        | TEXT    | Required |
| amount      | REAL    | Required |
| category    | TEXT    | Required |
| subcategory | TEXT    | Optional, default `''` |
| note        | TEXT    | Optional, default `''` |

---

## 🧪 Validation

Quick syntax validation:

```bash
python -m py_compile main.py
```

---

## 🔒 Notes

- Database write-check is performed during initialization.
- If database becomes read-only, tool responses include a clear error message.
- Keep `categories.json` versioned for consistent category behavior.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit changes
4. Open a pull request

---

## 📄 License

Add your preferred license file (`LICENSE`) and update this section accordingly.
