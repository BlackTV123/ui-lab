# ui-lab

Individual automated UI testing lab. Selected tool parts:

- Part 2: Selenium WebDriver in Java (`selenium-java/`; implementation pending).
- Part 3: Robot Framework (`robot/`; tests and two recorded QP-01 runs completed).

See [RESULTS.md](RESULTS.md) for the manual test results, tool results and reflection questions.

## Robot Framework

The `robot/` folder contains the first page-title test (`first.robot`), the web-form test (`web_form.robot`) and the complete QuickPizza test case QP-01 (`pizza_scenario.robot`). Reusable QuickPizza keywords and locators are kept in `robot/resources/quickpizza.resource`.

### Setup on Windows PowerShell

Requires Python 3.10 or newer, Google Chrome and a compatible ChromeDriver. The recorded runs used Python 3.13.12, Chrome 158.0.8127.37 and ChromeDriver 158.0.8127.36.

From the repository root:

```powershell
cd robot
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
$env:CHROMEDRIVER = "C:\drivers\chromedriver-win64\chromedriver.exe"
```

Set `CHROMEDRIVER` to the location of the driver on your computer. Keep the driver outside this repository. Activate the virtual environment and ensure the variable is set whenever using a new terminal.

### Run the tests

From the `robot/` folder with the virtual environment active, this command runs all three tests:

```powershell
robot first.robot web_form.robot pizza_scenario.robot
```

To run only QP-01:

```powershell
robot pizza_scenario.robot
```

QP-01 checks the home-page heading, the advanced fields, the entered restrictions, the recommendation, the login-required message and the matching pizza in the admin list. It uses a new timestamped pizza name on each run.

### Recorded evidence

Two separate headless runs were recorded using:

```powershell
robot -d results/run1 -v BROWSER:headlesschrome pizza_scenario.robot
robot -d results/run2 -v BROWSER:headlesschrome pizza_scenario.robot
```

Run these commands one at a time. Each command writes to its own folder and replaces any previous evidence in that folder.

- [Run 1 report](robot/results/run1/report.html) and [log](robot/results/run1/log.html): PASS; suite elapsed 11.908 seconds; pizza `Lab Pizza 20261118-225315`.
- [Run 2 report](robot/results/run2/report.html) and [log](robot/results/run2/log.html): PASS; suite elapsed 12.498 seconds; pizza `Lab Pizza 20261118-225437`.

Each run folder contains `output.xml`, `log.html`, `report.html` and screenshots for QP-01 steps 3, 4, 5 and 7. Keep both run folders in Git. The virtual environment and practice output written directly in `robot/` are excluded by `.gitignore`.
