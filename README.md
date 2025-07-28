# User-Provisioning
Contains script that reads a CSV file and updates existing HubSpot users’ team assignments and permission sets via the HubSpot API.

## 🔧 Features

- Updates the **Primary Team**, **Additional Teams**, and **Role (Permission Set)** for each user.
- Supports **dry run** mode to simulate changes before applying.
- Includes **rate limit handling** with exponential backoff.
- Logs progress every 100 users.

---

## 📄 CSV Format

The input CSV must have the **exact** following column headers (case-insensitive matching):

| Column Name      | Description                                 |
|------------------|---------------------------------------------|
| `Email`          | The user's email address (used to identify the user in HubSpot) |
| `Primary Team`   | The name of the team the user should primarily belong to |
| `Additional Teams` | Semi-colon (`;`) separated list of other team names |
| `Permission Set` | The name of the role to assign (case-insensitive) |

⚠️ **Important**:
- Column **names must match exactly** (spelling, spacing, and order) as above.
- **Team names** and **role names** must match exactly what exists in HubSpot or mapping will fail.

---

## 🚫 Super Admins

HubSpot does **not allow updates to Super Admin users via API**.  
If a user requires the **Super Admin** role, you'll need to manually assign it in the HubSpot UI.

---

## 🧪 Dry Run Mode

Use `--test` to simulate changes without applying them to HubSpot.  
This is useful to validate your mappings and catch potential issues before making real updates.

---

## ▶️ How to Run

### 1. Set your HubSpot API Key

In the script, edit the following line:

```python
HUBSPOT_API_KEY = "your-private-app-token"
```

### 3. Run the script
Basic usage:

python3 update_users.py --csv path/to/your_file.csv

Test mode:

python3 update_users.py --csv path/to/your_file.csv --test
