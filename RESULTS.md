# UI lab results

Tool parts that I chose: Part 2 - Selenium WebDriver in Java; Part 3 - Robot Framework.

## Part 0

- Step 0.1, Chrome version: 158.0.8127.37 (Official Build, 64-bit)
- Step 0.3, ChromeDriver version: 158.0.8127.36
- Step 0.4, locator of Pizza, Please!: `xpath=//button[normalize-space()='Pizza, Please!']`
- Step 0.4, locator of Excluded tools: `xpath=//label[normalize-space()='Excluded tools']/following-sibling::select`
- Step 0.4, locator of Must be vegetarian: `id=default-checkbox`
- Step 0.4, locator of Custom Pizza Name: `css=input#pizza-name`

All four locators were checked in Chrome DevTools Console. Each matched exactly one element.

### Step 0.5: QP-01 - A custom pizza reaches the admin list

Status: Manual QP-01 completed, 7 steps passed. Results were recorded from the observed output and the student's confirmation of the manual steps.

- Preconditions: QuickPizza is reachable and the browser is not logged in.
- Test data: maximum calories per slice `600`; excluded tool `Knife`; vegetarian checked; pizza name `Lab Pizza` followed by the date and time; admin username `admin`, password `admin`.
- Pizza name of the documented recommendation and matching admin entry: `Lab Pizza 20261118-213000`
- Tool shown in the recommendation: `Pizza cutter`
- Calories per slice shown in the recommendation: `425`
- Tool shown in the matching admin entry: `Pizza cutter` (ingredients_number=6)
- Earlier observations: Other admin-list observations for the same name included `Pizza cutter` and `Scissors`, both with ingredients_number=5. These are separate from the documented recommendation and matching admin entry above; they have not been established to refer to the same pizza record. Use a fresh date-and-time name for every future pizza request.

| Step | Action | Expected result | Actual result | Pass or fail |
|------|--------|-----------------|---------------|--------------|
| 1 | Open the QuickPizza home page. | The heading reads "Looking to break out of your pizza routine?" | The student confirmed that the heading "Looking to break out of your pizza routine?" appeared. | Pass |
| 2 | Turn on Advanced. | Max Calories per Slice, Excluded tools, Must be vegetarian and Custom Pizza Name appear. | The student confirmed that all four advanced fields appeared after turning on Advanced. | Pass |
| 3 | Enter 600, exclude Knife, check vegetarian, and enter a unique pizza name. | The fields show the entered values. | The student confirmed the calorie limit was 600, Knife was excluded, and vegetarian was checked. Custom Pizza Name was `Lab Pizza 20261118-213000`. | Pass |
| 4 | Click Pizza, Please! | The answer shows the entered pizza name, a tool other than Knife, and 600 or fewer calories per slice. | The recommendation shows `Lab Pizza 20261118-213000`, tool `Pizza cutter` (not Knife), and 425 calories per slice (at most 600). The result name matches the Custom Pizza Name field. | Pass |
| 5 | Click Love it! without logging in. | The page says "Please log in first." | The student confirmed that clicking Love it! without logging in displayed "Please log in first." | Pass |
| 6 | Open /admin and sign in with admin / admin. | The page shows "Latest pizza recommendations". | The admin page displayed "Latest pizza recommendations" and a Logout button. | Pass |
| 7 | Find the pizza name in the admin list. | The entry shows the same pizza name and the same tool as in step 4. | The admin list shows `Lab Pizza 20261118-213000 (tool=Pizza cutter, ingredients_number=6)`. Its name and tool match the recommendation in step 4. | Pass |

## Part 2: Selenium WebDriver in Java

- Step 2.4, the failure line for the wrong title: Pending
- Step 2.15, QP01Test run 1, result and time: Pending
- Step 2.15, QP01Test run 2, result and time: Pending
- Step 2.20, full run 1, time and number of tests: Pending
- Step 2.20, full run 2, time and number of tests: Pending

## Part 3: Robot Framework

- robot --version: `Robot Framework 7.5.1 (Python 3.13.12 on win32)`
- Step 3.2, failure message for the wrong title: `Title should have been 'Web Form' but was 'Web form'.` The deliberately incorrect title produced `1 test, 0 passed, 1 failed`. After restoring `Web form`, the student confirmed that the test passed again.
- Step 3.3, web form test: `1 test, 1 passed, 0 failed`. The recorded run passed the Submit click, the title check `Web form - target page`, and the message check `Received!`.
- Step 3.4, QuickPizza home page: The student reported `1 test, 1 passed, 0 failed`. The test opened QuickPizza, waited for its heading, and checked the heading text.
- Step 3.5, advanced fields: The student reported `1 test, 1 passed, 0 failed`. The test checked that the four advanced fields appeared, filled in 600 calories, excluded Knife, selected vegetarian and generated a timestamped pizza name, then checked all four input values.
- Step 3.6, recommendation: `1 test, 1 passed, 0 failed`. The recorded run used `Lab Pizza 20261118-224729`, returned tool `Pizza cutter` and 275 calories per slice. The name matched, the tool was not Knife and the calories were at most 600.
- Step 3.7, complete QP-01: The recorded run passed all seven steps. It created `Lab Pizza 20261118-224952`, with tool `Scissors` and 450 calories per slice. The login-required message, admin login, and the matching pizza name and tool in the admin list all passed.
- Step 3.8, run 1, result, elapsed time and pizza name: PASS (`1 test, 1 passed, 0 failed`); suite elapsed `00:00:11.908` (test elapsed `00:00:11.350`); pizza name `Lab Pizza 20261118-225315`; tool `Scissors`; calories per slice `500`. Evidence: [report](robot/results/run1/report.html), [log](robot/results/run1/log.html).
- Step 3.8, run 2, result, elapsed time and pizza name: PASS (`1 test, 1 passed, 0 failed`); suite elapsed `00:00:12.498` (test elapsed `00:00:11.781`); pizza name `Lab Pizza 20261118-225437`; tool `Scissors`; calories per slice `575`. Evidence: [report](robot/results/run2/report.html), [log](robot/results/run2/log.html).
- Step 3.8, evidence check: Both runs used headless Chrome and passed all seven QP-01 steps. Each run folder contains `output.xml`, `log.html`, `report.html` and four screenshots. The login-required message and the matching pizza entry are visible in the screenshots. The two runs used different timestamped names.

## Part B

Answer each question in three to six sentences, using evidence from the actual runs.

1. Why locate Max Calories per Slice through its label instead of its id? What page change would allow a reliable id locator, and why would it help? Answer: Pending
2. What kind of test oracle compares the tool in the admin list with the recommendation in QP-01 step 7? Give one fault it could catch. Answer: Pending
3. Propose a check that the pizza is vegetarian, and explain what information the check would need. Answer: Pending
4. Compare Selenium WebDriver in Java and Robot Framework using their waits, the time needed to write QP-01, and the readability of their reports or logs. Answer: Pending
5. Choose a tool for Project 2 and justify it with two reasons from this lab. Answer: Pending
6. Part 2: If the calories-box locator changes, what must change in QP01Test and QP01PageObjectTest? Why do page objects make the repair smaller? Answer: Pending
7. Part 3: Where would you change the calories-box locator, and how does the resource file keep that change out of the test file? Answer: Pending
