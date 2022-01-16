# Pewlett-Hackard-Analysis

### 1. Overview of Pewlett Hackard Analysis:
#### After querying our newly created database and summarizing information, we have a new task to tackle. We want to query our data to gather the likely employees who will be retiring as well as those who are eligible for a mentorship program.

### 2. Pewlett Hackard Analysis Results:
* 72,458 employees are eligible to retire.
* The majority of retiring titles are Senior members. There are 25,916 Engineers and 24,926 Staff. See breakdown below:
      ![retiring](https://github.com/maldonado91/Pewlett-Hackard-Analysis/blob/main/Resources/retiring_titles.PNG)
* 1,549 employees are eligible for the mentorship program
* The majority of mentorship titles are Senior members. There are 569 Staff and 529 Engineers. See breakdown below: 
      ![mentorship](https://github.com/maldonado91/Pewlett-Hackard-Analysis/blob/main/Resources/mentorship_titles.PNG)

 ### 3 Summary:
#### 
* How many roles will need to be filled as the "silver tsunami begins to make an impact?
      Pewlett Hackard is looking at just over 72,000 positions that will need to be filled if all eligible employees choose to retire.
* Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
      I would say yes because there are double the amount of Senior Engineers/Staff and than no-Seniors level employees.
* Two additional queries/tables that would provide insight into the upcoming "silver tsunami"?

      I did a GROUB BY of all mentorship eligible employes to view that breakdown like we did retirement eligible employees
           
           
           ```
           --Create mentorship titles table
            DROP TABLE IF EXISTS mentorship_titles;
            SELECT COUNT(title), title 
            INTO mentorship_titles
            FROM mentorship_eligibility
            GROUP BY title
            ORDER BY COUNT(title) DESC;

            SELECT * FROM mentorship_titles; 
            ```
            
      Since most of the elibible retirees are Engineers and Staff I'm curious to see how many non retiring elibigle employees will be left to fill those potential job openings
           
           
           ```
            --Create new NON retirement_titles table
            --Drop if already exists
            DROP TABLE IF EXISTS non_retirement_titles;
            --Enter data from employees and titles tables
            SELECT e.emp_no, e.first_name, e.last_name, et.title, et.from_date, et.to_date
            INTO non_retirement_titles
            FROM employees e
            LEFT JOIN titles et ON et.emp_no = e.emp_no
            WHERE e.birth_date NOT BETWEEN '1952-01-01' AND '1955-12-31'
            ORDER BY e.emp_no;

            --Select new non retirement table
            SELECT * FROM non_retirement_titles;

            --Use Dictinct with Orderby to remove duplicate rows
            DROP TABLE IF EXISTS unique_nonret_titles;
            SELECT DISTINCT ON (emp_no) emp_no,
            first_name,
            last_name,
            title
            INTO unique_nonret_titles
            FROM non_retirement_titles
            WHERE to_date = '9999-01-01'
            ORDER BY emp_no, to_date DESC;

            SELECT * FROM unique_nonret_titles;

            --Create retiring titles table
            DROP TABLE IF EXISTS non_retiring_titles;
            SELECT COUNT(title), title 
            INTO non_retiring_titles
            FROM unique_nonret_titles
            GROUP BY title
            ORDER BY COUNT(title) DESC;

            SELECT * FROM non_retiring_titles; 
            ```
