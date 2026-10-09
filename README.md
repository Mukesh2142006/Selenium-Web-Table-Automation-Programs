# Selenium Web Table Automation

## About the Project

This project contains four Python Selenium programs to automate web table operations using the website [The Internet - Tables](https://the-internet.herokuapp.com/tables).

The programs demonstrate how to read table data, extract employee details, search for an employee, and count the number of rows and columns.

## Technologies Used

* Python
* Selenium WebDriver
* Google Chrome
* VS Code

## Programs Included

### 1. Read All Table Data

* Opens the web table page.
* Finds the table using its ID.
* Reads all rows, including the header.
* Prints the table data.

```

from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")
    driver.maximize_window()
    table = driver.find_element(By.ID, "table1")
    rows = table.find_elements(By.TAG_NAME, "tr")
    print("Total rows including header:", len(rows))
    for row in rows:
        cells = row.find_elements(By.TAG_NAME, "th")

        if not cells:
            cells = row.find_elements(By.TAG_NAME, "td")

        row_data = [cell.text for cell in cells]
        print(row_data)

finally:
    driver.quit()
```
## OUTPUT:
<img width="1007" height="680" alt="image" src="https://github.com/user-attachments/assets/8b268a16-1e8d-48fd-9e8b-31140fdffa2d" />

### 2. Extract First Row Details

* Finds the table data rows.
* Extracts the first data row.
* Prints the last name, first name, and email.

```
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    table = driver.find_element(By.ID, "table1")

    # Get all data rows, excluding the header
    rows = table.find_elements(By.CSS_SELECTOR, "tbody tr")

    # First data row
    first_row = rows[0]

    # Get all cells in the row
    cells = first_row.find_elements(By.TAG_NAME, "td")

    # First column: Last Name
    print("Last Name:", cells[0].text)

    # Second column: First Name
    print("First Name:", cells[1].text)

    # Third column: Email
    print("Email:", cells[2].text)

finally:
    driver.quit()
```
## OUTPUT:
<img width="1452" height="998" alt="image" src="https://github.com/user-attachments/assets/35a50eb4-e327-46c5-a59e-0cc0b5210ac8" />

### 3. Search Employee by Name

* Searches for an employee using the first name.
* Prints the employee details if found.
* Displays a message if the employee is not found.
```

from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    rows = driver.find_elements(
        By.CSS_SELECTOR, "#table1 tbody tr"
    )

    search_name = "John"
    found = False

    for row in rows:
        cells = row.find_elements(By.TAG_NAME, "td")

        first_name = cells[1].text

        if first_name == search_name:
            print("Employee found!")
            print("Employee details:", row.text)
            found = True
            break

    if not found:
        print("Employee not found")

finally:
    driver.quit()
```
## OUTPUT:
<img width="1455" height="998" alt="image" src="https://github.com/user-attachments/assets/26e32fa8-08f7-4aa8-9786-d25967a47cc4" />

### 4. Count Rows and Columns

* Counts the number of data rows.
* Counts the number of table columns.
* Prints the results.


```
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    table = driver.find_element(By.ID, "table1")

    rows = table.find_elements(By.CSS_SELECTOR, "tbody tr")
    headers = table.find_elements(By.CSS_SELECTOR, "thead th")

    print("Number of data rows:", len(rows))
    print("Number of columns:", len(headers))

finally:
    driver.quit()
```
## OUTPUT:
<img width="1442" height="997" alt="image" src="https://github.com/user-attachments/assets/1e1f2535-0849-471c-948e-bd39d704bd56" />
