# Git Workflow Demo: Python Calculator

This demo shows how multiple developers contribute features to a shared `calculator.py` program.

## 🎭 The Scenario

-   **Base State**: `integration` branch has **Add** and **Subtract**.
-   **User A**: Adds **Multiply** (Branch: `feat/multiply`).
-   **User B**: Adds **Divide** (Branch: `feat/divide`).

**The Conflict**: Both users add their new option as **"Item 3"** in the menu. When you try to merge both, Git won't know which "Item 3" is correct!

---

## ✅ Phase 1: Setup

1.  Open terminal in `d:\SampleRepo\GitBranchingDemo`.
2.  Run: `.\Setup_Demo_Repo.ps1`
3.  **GitHub Setup**:
    -   Create a NEW empty repo on GitHub.
    -   Run:
        ```powershell
        git remote remove origin
        git remote add origin <YOUR_GITHUB_URL>
        git push -u origin --all
        ```

---

## 🚀 Phase 2: The Demo Flow

### Step 1: Merge 'Multiply' (Clean)
1.  Go to GitHub -> **v New Pull Request**.
2.  **Base**: `integration` | **Compare**: `feat/multiply`.
3.  Notice it creates **Item 3: Multiply** in the menu.
4.  **Create** and **Merge** the Pull Request.

### Step 2: Merge 'Divide' (Conflict)
1.  **New Pull Request**.
2.  **Base**: `integration` | **Compare**: `feat/divide`.
3.  **Conflict Alert!** GitHub says it cannot merge automatically.
4.  Click **"Resolve conflicts"**.

### Step 3: Resolving the Menu Conflict
You will see conflicts in `calculator.py`.

**The Situation**:
-   User A added `multiply` as Item 3.
-   User B added `divide` as Item 3.

**The Fix**:
1.  Keep **both** function definitions (`def multiply` AND `def divide`).
2.  Fix the Menu:
    -   Keep "3. Multiply".
    -   Change "3. Divide" to **"4. Divide"**.
3.  Fix the Logic:
    -   Ensure the `if/elif` block handles both choice '3' and choice '4'.
4.  Remove `<<<<<<<`, `=======`, `>>>>>>>` lines.

**Example Final Code**:
```python
    print("3. Multiply")
    print("4. Divide")  # Renumbered!

    # ... down in logic ...
    elif choice == '3':
        # ... multiply code ...
    elif choice == '4':
        # ... divide code ...
```
5.  **Mark as Resolved** -> **Commit Merge**.

---

## 🔁 Reset
To try again:
1.  Run `.\Setup_Demo_Repo.ps1`
    -   *Note: The script tries to preserve your remote URL. If it says "Restoring remote origin...", you can skip to step 3.*
2.  If the script didn't find the remote (or it's your first run), add it:
    ```powershell
    git remote add origin <YOUR_GITHUB_URL>
    ```
3.  **Force Push** to reset GitHub:
    ```powershell
    git push --force --all origin
    ```
