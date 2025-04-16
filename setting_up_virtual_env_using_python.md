
Python 3.3+ comes with `venv` built-in — no need to install anything else.

---

## 🚀 Step-by-Step Instructions

### 🔹 Step 1: Create a Virtual Environment

Navigate to your project folder:

```bash
cd path/to/your/project
```

Then run:

```bash
python -m venv venv
```

> This creates a folder called `venv/` with a self-contained Python environment.

---

### 🔹 Step 2: Activate the Environment

#### 🪟 On **Windows**:
```bash
venv\Scripts\activate
```

#### 🐧 On **Linux/macOS**:
```bash
source venv/bin/activate
```

✅ You'll know it's activated if your terminal prompt starts with:
```
(venv)
```

---

### 🔹 Step 3: Install Dependencies

Once activated, install your packages using `pip`:

```bash
pip install numpy pandas matplotlib
```

---

### 🔹 Step 4: Freeze Your Environment (Optional)

Save current packages to a file:

```bash
pip freeze > requirements.txt
```

To recreate the environment later:

```bash
pip install -r requirements.txt
```

---

### 🔹 Step 5: Deactivate the Environment

When you're done:

```bash
deactivate
```

---

## 🧠 Bonus Tips

| Task | Command |
|------|---------|
| Delete environment | Just delete the `venv/` folder |
| Check where pip installs | `which pip` (mac/Linux), `where pip` (Windows) |
| Use environment in VSCode | It will auto-detect or use `Python: Select Interpreter` |

---

## ✅ TL;DR Cheat Sheet

```bash
# Create environment
python -m venv venv

# Activate (Linux/macOS)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate

# Install packages
pip install -r requirements.txt

# Deactivate
deactivate
```

---
