================================================================================
TERMINAL-BENCH 2 TASK FIX - SUBMISSION PACKAGE
================================================================================

Project: Fix broken Harbor task (dynamo/log-report)
Status: ✅ COMPLETE - All 9 defects identified and fixed

================================================================================
START HERE
================================================================================

1. Read QUICK_REFERENCE.txt (2 minutes)
   → Understand what changed and how to submit

2. Read DEFECT_REPORT.txt (5-10 minutes)
   → Deep dive into each defect and its fix

3. Use SUBMISSION_BOXES.txt (copy-paste ready)
   → Plain text content for each submission box

4. Reference other docs as needed:
   → COMPLETE_SUBMISSION.txt (everything in one file)
   → FIXES_SUMMARY.md (table format)
   → INDEX_AND_GUIDE.txt (comprehensive guide)

================================================================================
FILES IN THIS PACKAGE
================================================================================

📖 DOCUMENTATION:
  • README.txt ......................... This file
  • QUICK_REFERENCE.txt ............... Quick summary and next steps
  • DEFECT_REPORT.txt ................. Detailed defect analysis
  • FIXES_SUMMARY.md .................. Summary table
  • INDEX_AND_GUIDE.txt ............... Comprehensive guide
  • COMPLETE_SUBMISSION.txt ........... All files in one document
  • SUBMISSION_BOXES.txt .............. Copy-paste ready for forms

📦 CORRECTED FILES (individual):
  • 01_task.toml ...................... Fixed task.toml
  • 02_instruction.md ................. Fixed instruction.md
  • 03_environment_Dockerfile ......... Fixed environment/Dockerfile
  • 04_solution_solve.sh .............. OK (no changes)
  • 05_solution_solve.py .............. OK (no changes)
  • 06_tests_test.sh .................. Fixed tests/test.sh
  • 07_tests_test_outputs.py .......... Fixed tests/test_outputs.py

================================================================================
9 DEFECTS FOUND AND FIXED
================================================================================

environment/Dockerfile:
  1.1 ❌ Non-reproducible base image (python:latest)
      → ✅ Pinned to python:3.11-slim@sha256:e4d4e1c0c...
  
  1.2 ❌ Leaked solution (COPY solution_hint.py)
      → ✅ Removed to prevent agent cheating
  
  1.3 ❌ Missing directories (/solution, /tests)
      → ✅ Added with RUN mkdir -p

task.toml:
  2.1 ❌ Artifact path mismatch (/app/out.json vs /app/report.json)
      → ✅ Changed to /app/report.json

tests/test_outputs.py:
  3.1 ❌ No JSON validation
      → ✅ Added test_report_valid_json()
  
  3.2 ❌ No schema validation
      → ✅ Added test_report_has_required_keys()
  
  3.3 ❌ No semantic correctness check
      → ✅ Added test_report_correct_values()

tests/test.sh:
  4.1 ❌ Wrong reward path (/app/reward.txt)
      → ✅ Changed to /logs/verifier/reward.txt

instruction.md:
  5.1 ❌ No numbered success criteria
      → ✅ Added 5 explicit, verifiable criteria

================================================================================
HOW TO USE THIS PACKAGE
================================================================================

OPTION A: Copy individual files
  1. Open numbered files (01_, 02_, etc.)
  2. Copy content to correct locations in your log-report/ directory
  3. Test locally with Harbor
  4. Push to GitHub
  5. Submit

OPTION B: Use complete submission file
  1. Open COMPLETE_SUBMISSION.txt
  2. Follow the directory structure shown
  3. Extract all files from sections
  4. Test and submit

OPTION C: Copy-paste into submission form
  1. Open SUBMISSION_BOXES.txt
  2. Copy each box's content to submission form
  3. Paste GitHub link
  4. Submit

================================================================================
KEY CHANGES SUMMARY
================================================================================

Changed Files:
  ✏️  environment/Dockerfile - 3 fixes (base image, leaked solution, directories)
  ✏️  task.toml - 1 fix (artifact path)
  ✏️  instruction.md - 1 fix (added success criteria)
  ✏️  tests/test.sh - 1 fix (reward path)
  ✏️  tests/test_outputs.py - 3 additions (validation tests)

Unchanged Files:
  ✓  solution/solve.py (correct)
  ✓  solution/solve.sh (correct)
  ✓  environment/access.log (test data correct)

================================================================================
VERIFICATION CHECKLIST
================================================================================

Before submission, test locally:

□ Test 1: oracle agent should PASS
  harbor run -p log-report -a oracle
  Expected: reward.txt contains "1"

□ Test 2: nop agent should FAIL
  harbor run -p log-report --agent nop
  Expected: reward.txt contains "0"

□ Reproducibility checks
  grep "python:latest" Dockerfile → 0 results
  grep "solution_hint" Dockerfile → 0 results
  head -1 Dockerfile | grep "@sha256" → found

□ Path checks
  grep "out.json" task.toml → 0 results
  grep "report.json" task.toml → found
  grep "/logs/verifier/reward.txt" test.sh → found

□ Test coverage
  wc -l test_outputs.py → should be ~60 lines (was ~10)
  grep "def test_" test_outputs.py → should be 5 functions

All checks pass? You're ready to submit!

================================================================================
SUBMISSION STEPS
================================================================================

1. Create corrected task structure:
   log-report/
   ├── task.toml (FIXED)
   ├── instruction.md (FIXED)
   ├── environment/
   │   ├── Dockerfile (FIXED)
   │   └── access.log (OK)
   ├── solution/
   │   ├── solve.sh (OK)
   │   └── solve.py (OK)
   └── tests/
       ├── test.sh (FIXED)
       └── test_outputs.py (FIXED)

2. Test with Harbor locally:
   harbor run -p log-report -a oracle     # Should PASS
   harbor run -p log-report --agent nop   # Should FAIL

3. Create GitHub repository:
   git init
   git add -A
   git commit -m "Fix: Harbor task defects"
   git push origin main

4. In submission form, paste:
   Box 1: Content of 01_task.toml
   Box 2: Content of 02_instruction.md
   Box 3: Content of 03_environment_Dockerfile
   Box 4: Content of 06_tests_test.sh
   Box 5: Content of 07_tests_test_outputs.py
   Box 6: https://github.com/YOUR-USERNAME/log-report-fixed

5. After passing:
   git config --local visibility private
   (Or via GitHub web UI)

================================================================================
DEFECT CATEGORIES
================================================================================

REPRODUCIBILITY (1 defect):
  • Non-pinned base image

SECURITY (1 defect):
  • Leaked solution to agent

HARBOR COMPLIANCE (3 defects):
  • Missing directory structure
  • Artifact path mismatch
  • Wrong reward path

HONEST GRADING (3 defects):
  • No JSON validation
  • No schema validation
  • No semantic correctness check

CLARITY (1 defect):
  • No numbered success criteria

All categories addressed. Task now meets Harbor standards.

================================================================================
EXPECTED BEHAVIOR
================================================================================

Oracle Agent (reference solution):
  ✅ Reads access.log (6 entries)
  ✅ Counts total requests: 6
  ✅ Counts unique IPs: 3 (192.168.0.1, 192.168.0.2, 10.0.0.5)
  ✅ Finds top path: /index.html (appears 3 times)
  ✅ Writes valid JSON to /app/report.json
  ✅ All 5 tests pass
  ✅ Reward: 1

No-Op Agent:
  ✅ Does nothing
  ❌ No report.json created
  ❌ test_report_exists() fails immediately
  ✅ Reward: 0

Verifier Behavior:
  ✅ Reports reward to /logs/verifier/reward.txt
  ✅ Harbor can read and verify result
  ✅ Task is graded honestly

================================================================================
QUESTIONS?
================================================================================

For details on each defect:
  → See DEFECT_REPORT.txt (comprehensive analysis)

For quick reference:
  → See QUICK_REFERENCE.txt

For submission content:
  → See SUBMISSION_BOXES.txt or individual numbered files

For everything in one place:
  → See COMPLETE_SUBMISSION.txt

================================================================================

Ready to submit? Start with QUICK_REFERENCE.txt, then use SUBMISSION_BOXES.txt
for copy-paste content.

Good luck! 🚀

================================================================================
