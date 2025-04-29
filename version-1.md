```
START
  |
  v
[1️⃣ User Starts Session]
  - User opens chatbot, CLI, or web UI.
  - Chooses: 
    a) Create New Trade File
    b) Modify Existing Trade File
  |
  v
[2️⃣ Dynamic Prompt Builder]
  - Show only mandatory fields for input:
    - Trade Date
    - Settlement Date
    - Safekeeping Account
    - Branch
    - Securities / ISIN
    - Instruction Type (RF, DF, RVP, DVP)
    - Transaction Type (Standard, Repo, Reverse Repo, Pledge, etc.)
  - Prompt example auto-generated:
    → "Create a DVP Repo trade for ISIN IN1234567890 with settlement on May 2, using account ABC123 at Mumbai branch."
  |
  v
[3️⃣ User Enters Prompt or Data]
  - User fills mandatory fields via form or free text prompt
  - May optionally provide quantity, currency, counterparty, etc.
  |
  v
[4️⃣ Search Vector DB for Similar Trades]
  - Embed prompt context
  - Fetch user’s past N trade vectors with similar context
  - Return trade patterns (e.g., typically uses ABC Bank for bonds)
  |
  v
[5️⃣ LLM Engine Completes Trade Instruction]
  - Uses:
    • User input
    • Vector DB matches
    • Domain-specific trade logic
  - Fills all ~200 fields, even optional ones
  - Adds notes where values are inferred
  |
  v
[6️⃣ File Generator: Excel/CSV Output]
  - Map completed fields into your org’s existing trade file format
  - Output formats:
    • CSV (.csv)
    • Excel (.xlsx)
  |
  v
[7️⃣ User Reviews and Edits]
  - Preview structured table in UI
  - Can edit inline or regenerate with new prompt
  |
  v
[8️⃣ Export Options]
  - Option 1: Download file (CSV/Excel)
  - Option 2: Upload directly to trade system (if integrated)
  |
  v
✅ END
```
