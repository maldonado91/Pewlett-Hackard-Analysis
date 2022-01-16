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
* Two additional queries/tables thatwould provide insight into the upcoming "silver tsunami"?
      - I did a GROUB BY of all mentorship eligible employes to view that breakdwn like we did retirement eligible employees
           
           ```
            DROP TABLE IF EXISTS mentorship_titles;
            SELECT COUNT(title), title 
            INTO mentorship_titles
            FROM mentorship_eligibility
            GROUP BY title
            ORDER BY COUNT(title) DESC;

            SELECT * FROM mentorship_titles; 
            ```
            
 Markup : * Bullet list
              * Nested bullet
                  * Sub-nested bullet etc
