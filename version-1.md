** GenAI-Based Trade File Creator (Excel/CSV)**

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
  - mandatory fields input:
    - Trade Date
    - Settlement Date
    - Safekeeping Account
    - Branch
    - Securities / ISIN
    - Instruction Type (RF, DF, RVP, DVP)
    - Transaction Type (Standard, Repo, Reverse Repo, Pledge, etc.)
  - Prompt example auto-generated:
    → "Create a DVP Repo trade for ISIN IN1234567890 with settlement on May 2, using account ABC123 at NK branch."
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
  - Return trade patterns 
  |
  v
[5️⃣ LLM Engine Completes Trade Instruction]
  - Uses:
    • User input
    • Vector DB matches
    • Domain-specific trade logic
  - Fills at max fields, have approx ~200 fields, many optional
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

**Alternate Flow: Modify Existing File**
```
User uploads Excel/CSV file
  |
  v
LLM parses file → identifies records
  |
  v
User prompt: “Change settlement date to May 5 and counterparty to XYZ”
  |
  v
LLM updates only relevant fields
  |
  v
New Excel/CSV file generated → preview → download/upload
```


**Flow chart**

```mermaid
flowchart TD
    A[Start] --> B[User Starts Session: New File or Modify File]
    B --> C[Dynamic Prompt Builder: Mandatory Fields Only]
    C --> D[User Provides Prompt or Input]
    D --> E[Search Vector DB for Similar Past Trades]
    E --> F[LLM Completes Trade Instruction (200 Fields)]
    F --> G[Map Output to CSV or Excel Template]
    G --> H[User Previews and Edits (Optional)]
    H --> I[Export File: Download or Upload]
    I --> Z[End]

    subgraph Alternate Flow: Modify Existing File
        M1[User Uploads Existing File] --> M2[LLM Parses File]
        M2 --> M3[User Provides Update Prompt]
        M3 --> M4[LLM Updates Relevant Fields]
        M4 --> G
    end
```

**Service to Service**

```mermaid
flowchart TD
    A[Start: User Enters Prompt or Uploads File] --> B[Prompt Parsing Service]
    B --> C[Embedding Generator]
    C --> D[Vector DB Search Service]
    D --> E[Similar Trade Patterns Returned]
    E --> F[LLM Completion Service]
    F --> G[Field Completion & Trade Logic Service]
    G --> H[Template Mapping Service (CSV/Excel Formatter)]
    H --> I[File Generation Service]
    I --> J[Preview & Edit UI Service]
    J --> K[Export Service (Download / Upload to Trade System)]
    K --> Z[End]
```

