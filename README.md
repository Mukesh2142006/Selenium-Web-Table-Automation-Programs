# Selenium Web Table Automation

## About the Project

This project contains eight Python Selenium programs to automate web table operations using the website [The Internet - Tables](https://the-internet.herokuapp.com/tables).

The programs demonstrate how to print column headings, extract employee records, search by last name, extract email addresses, find the highest Due amount, verify website links, and count data rows.

## Technologies Used

* Python
* Selenium WebDriver
* Google Chrome
* VS Code

## Programs Included

## 1. Print All Column Headings

* Opens the web table page.
* Locates all column headings.
* Prints the headings displayed in the table.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")
    driver.maximize_window()

    headers = driver.find_elements(By.CSS_SELECTOR, "#table1 thead th")
    print("Column Headings:")

    for header in headers:
        print(header.text)

finally:
    driver.quit()
```

## OUTPUT:

<img width="1455" height="952" alt="image" src="https://github.com/user-attachments/assets/564e8fea-b491-49f6-8151-aca8649536c5" />


---

## 2. Print the First Data Row

* Finds the first data row inside the table.
* Extracts all cells from the first row.
* Prints the first employee record.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    first_row = driver.find_element(By.CSS_SELECTOR, "#table1 tbody tr:first-child")
    cells = first_row.find_elements(By.TAG_NAME, "td")

    print("First Data Row Data:")
    row_data = [cell.text for cell in cells]
    print(row_data)

finally:
    driver.quit()
```

## OUTPUT:

<img width="488" height="323" alt="image" src="https://github.com/user-attachments/assets/e754c803-a918-4ac9-96f1-c4ee012753e3" />


---

## 3. Print the Last Data Row

* Finds all data rows in the table.
* Selects the last data row.
* Prints the last employee record.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    rows = driver.find_elements(By.CSS_SELECTOR, "#table1 tbody tr")

    if rows:
        last_row = rows[-1]
        cells = last_row.find_elements(By.TAG_NAME, "td")

        print("Last Data Row Data:")
        row_data = [cell.text for cell in cells]
        print(row_data)

finally:
    driver.quit()
```

## OUTPUT:

<img width="570" height="388" alt="image" src="https://github.com/user-attachments/assets/215751ac-6411-4aed-baef-ba36df3fb0c2" />


---

## 4. Search for an Employee by Last Name

* Searches for an employee using the last name `Smith`.
* Prints the employee details if a match is found.
* Displays a message if the employee is not found.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    rows = driver.find_elements(By.CSS_SELECTOR, "#table1 tbody tr")
    search_last_name = "Smith"
    found = False

    for row in rows:
        cells = row.find_elements(By.TAG_NAME, "td")
        last_name = cells[0].text

        if last_name == search_last_name:
            print(f"Employee found with last name '{search_last_name}':")
            print("Employee details:", row.text)
            found = True
            break

    if not found:
        print("Employee not found")

finally:
    driver.quit()
```

## OUTPUT:

<img width="337" height="234" alt="image" src="https://github.com/user-attachments/assets/265af601-6c50-4404-8980-b72b6f62a6ca" />


---

## 5. Extract All Email Addresses

* Finds all employee data rows.
* Extracts email addresses from the third column.
* Prints all email addresses.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    rows = driver.find_elements(By.CSS_SELECTOR, "#table1 tbody tr")
    print("Extracted Email Addresses:")

    for row in rows:
        cells = row.find_elements(By.TAG_NAME, "td")
        email = cells[2].text
        print(email)

finally:
    driver.quit()
```

## OUTPUT:

<img width="449" height="289" alt="image" src="https://github.com/user-attachments/assets/3207f8ea-ca2b-4716-b687-229a741a0c5e" />


---

## 6. Find the Employee with the Highest Due Amount

* Retrieves all employee records.
* Extracts the Due amount from the fourth column.
* Converts the Due amount into a numeric value.
* Identifies and prints the employee with the highest Due amount.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    rows = driver.find_elements(By.CSS_SELECTOR, "#table1 tbody tr")
    max_due = -1.0
    max_due_employee = None

    for row in rows:
        cells = row.find_elements(By.TAG_NAME, "td")
        due_text = cells[3].text.replace("$", "")
        due_amount = float(due_text)

        if due_amount > max_due:
            max_due = due_amount
            max_due_employee = row.text

    print(f"Highest Due Amount: ${max_due:.2f}")
    print("Employee Details:", max_due_employee)

finally:
    driver.quit()
```

## OUTPUT:

<img width="363" height="250" alt="image" src="https://github.com/user-attachments/assets/38254668-b702-4736-9697-ae7d077e4bbb" />


---

## 7. Verify That a Particular Website Link Exists

* Retrieves website links from the table.
* Compares each link with the target URL.
* Prints `Pass` if the link exists.
* Prints `Fail` if the link is not found.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    target_url = "http://www.jsmith.com"
    links = driver.find_elements(By.CSS_SELECTOR, "#table1 tbody tr td a")

    found = False

    for link in links:
        href = link.get_attribute("href")

        if href == target_url:
            print(f"Pass: Website link found -> {href}")
            found = True
            break

    if not found:
        print(f"Fail: Website link '{target_url}' not found.")

finally:
    driver.quit()
```

## OUTPUT:

<img width="332" height="219" alt="image" src="https://github.com/user-attachments/assets/66e191c1-abbb-4160-bea3-8c9f9a388d2f" />


---

## 8. Count Data Rows Without Counting the Header

* Finds all data rows inside the `tbody` element.
* Excludes the header row from the count.
* Prints the total number of data rows.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

try:
    driver.get("https://the-internet.herokuapp.com/tables")

    rows = driver.find_elements(By.CSS_SELECTOR, "#table1 tbody tr")
    print("Number of data rows (excluding header):", len(rows))

finally:
    driver.quit()
```

## OUTPUT:

<img width="384" height="252" alt="image" src="https://github.com/user-attachments/assets/22029972-671e-4cff-b789-eb2108c4b645" />


---

## Conclusion

This project demonstrates eight Selenium WebDriver programs for web table automation. It covers locating elements, extracting table data, searching employee records, comparing Due amounts, verifying website links, and counting data rows using Python.
