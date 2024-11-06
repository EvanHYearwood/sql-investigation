<h1 align="center">SQL-Driven Security Analysis: Employee Login and Machine Access Patterns</h1>
<h2>Evan H. Yearwood - Portfolio Project</h2>

<h3>Project Description</h3>
<p>In this project, using the Google Virtual Lab Environment, I take on the role of a security professional in a large organization. My job is to investigate security issues. I’ve recently discovered some potential security issues involving login attempts and employee machines.</p>
<p>My task is to examine the organization’s data using SQL queries. This project aims to demonstrate my knowledge and technical ability in using SQL queries and filters to retrieve records from different datasets and investigate potential security issues.</p>
<p>For each task, I will describe how and why I used a specific query in the scenario.</p>

<h3>Task Overview</h3>
<p>This analysis covers multiple SQL-driven tasks designed to examine potential security concerns. Here’s an overview of each task:</p>
<ul>
  <li><strong>Task 1:</strong> Retrieve failed login attempts that occurred after business hours to identify suspicious activity outside working hours.</li>
  <li><strong>Task 2:</strong> Retrieve all login attempts on specific dates to investigate events surrounding a suspicious incident.</li>
  <li><strong>Task 3:</strong> Retrieve login attempts originating from outside of Mexico, focusing on international access patterns.</li>
  <li><strong>Task 4:</strong> Retrieve employees in the Marketing department within the East Building, cross-referencing with device data to ensure machine security compliance.</li>
  <li><strong>Task 5:</strong> Retrieve employee data for those in Finance or Sales departments to assist with security updates on machines used by these employees.</li>
  <li><strong>Task 6:</strong> Retrieve all employees not in the IT department to target this group for a specific security update.</li>
</ul>

<h2>Tasks</h2>

<h3>Task 1 - Retrieving After Hours Failed Login Attempts</h3>
<p><strong>Scenario:</strong> I’ve recently discovered a potential security incident that occurred after hours. In order to investigate this properly, I will be querying the <code>log_in_attempts</code> table and reviewing the <code>login_time</code> column. This way, I can have a full picture of what is going on. This will require using operators and filters to retrieve the relevant data for my query.</p>
<p>In this scenario, business hours end at 18:00, so our query will begin after that time.</p>

<h4>1st Query Command:</h4>

<img width="753" alt="Screen Shot 2024-11-06 at 12 48 11 AM" src="https://github.com/user-attachments/assets/7bc227dd-150e-4173-a52f-3376f9bcb868">

<p>Query Results:</p>

<img width="630" alt="Screen Shot 2024-11-06 at 12 49 19 AM" src="https://github.com/user-attachments/assets/a35666a1-1914-4efd-b28f-28d677edee4c">

<p><strong>Explanation:</strong> Within the <code>WHERE</code> clause, I used the exclusive <code>></code> operator to filter the data within the <code>login_time</code> column. From this queried data, I observed 39 total login attempts after business hours on various dates from 05/08-05/12. Many login attempts were successful, but I am only interested in the failed attempts, so I refine the query.</p>

<h4>2nd Query Command:</h4>

<img width="631" alt="Screen Shot 2024-11-06 at 12 49 44 AM" src="https://github.com/user-attachments/assets/489bf371-95e0-46fd-8c57-7b4409019ae8">

<p>Query Results:</p>
<p><strong>Explanation:</strong> I refined the query by including an <code>AND</code> filter and adding the condition <code>success = 0</code>. This refined data now provides a clearer picture of the failed login attempts after hours, aiding in further investigation into potential threats or helping to reduce our attack surface by deactivating old accounts attempting unauthorized access.</p>

<img width="628" alt="Screen Shot 2024-11-06 at 12 50 06 AM" src="https://github.com/user-attachments/assets/e847e412-5169-4be0-a980-fb0897f200f8">

<hr>

<h3>Task 2 - Retrieving Login Attempts on Specific Dates</h3>
<p><strong>Scenario:</strong> After conducting further investigation, our team noticed a suspicious event on 2022-05-09. We decided to focus on ALL login attempts made on this date and the date prior. To assist my team, I queried all login attempts on these dates, including successful ones.</p>

<h4>1st Query Command:</h4>

<img width="633" alt="Screen Shot 2024-11-06 at 12 56 36 AM" src="https://github.com/user-attachments/assets/40a9239b-ca08-46fc-8d2c-d0f20dda050d">

<p>Query Results:</p>

<img width="546" alt="Screen Shot 2024-11-06 at 12 57 27 AM" src="https://github.com/user-attachments/assets/3a899d0f-1473-4f25-af22-9cd9f93d2c16">

<p><strong>Explanation:</strong> Since we were querying two separate dates, I used the <code>OR</code> operator to include both conditions—dates 05-08 and 05-09. I did not need to add any conditions regarding login success for this part of the investigation.</p>

<hr>

<h3>Task 3 - Retrieving Login Attempts Outside of Mexico</h3>
<p><strong>Scenario:</strong> Our team has shifted its attention, as we believe the suspicious login activity we observed did not originate from Mexico. Now, I will investigate login attempts that occurred outside of Mexico.</p>

<h4>1st Query Command:</h4>

<img width="632" alt="Screen Shot 2024-11-06 at 12 57 53 AM" src="https://github.com/user-attachments/assets/d4f4a6cc-334e-401c-87ab-85af3f9324c9">

<p>Query Results:</p>

<img width="629" alt="Screen Shot 2024-11-06 at 12 58 26 AM" src="https://github.com/user-attachments/assets/2ce15931-c73b-4b78-814c-c0851b9e8884">

<p><strong>Explanation:</strong> To show results excluding Mexico, I added <code>WHERE NOT</code> to the command. Since not every country record was written exactly as "Mexico," I used the <code>LIKE</code> filter with the <code>%</code> wildcard to filter out all records starting with "Mex," covering variants like "Mexico."</p>

<hr>

<h3>Task 4 - Retrieving Employees in Marketing</h3>
<p><strong>Scenario:</strong> My team wants to perform security updates on specific employee machines in the Marketing department within the East Building. I will query all employees in this department and building and then cross-reference their <code>employee_id</code> with their <code>device_id</code> in the <code>machines</code> table.</p>

<h4>1st Query Command:</h4>

<img width="631" alt="Screen Shot 2024-11-06 at 12 58 55 AM" src="https://github.com/user-attachments/assets/784399ea-b5f3-43aa-859b-b69fb8e6ba41">

<p>Query Results:</p>

<img width="631" alt="Screen Shot 2024-11-06 at 12 59 10 AM" src="https://github.com/user-attachments/assets/eb57a13d-6507-4622-be90-d90dd73dd7d6">

<p><strong>Explanation:</strong> For this query, I used two conditions: "Marketing" for the department and "East%" for the office, using the <code>%</code> wildcard to cover all offices in the East Building. After retrieving all <code>employee_id</code> numbers, I used the <code>IN</code> operator in the next command.</p>

<h4>2nd Query Command:</h4>

<img width="630" alt="Screen Shot 2024-11-06 at 12 59 24 AM" src="https://github.com/user-attachments/assets/0083be32-39f3-438d-aa1e-1ee5e38070db">

<p>Query Results:</p>

<img width="630" alt="Screen Shot 2024-11-06 at 12 59 39 AM" src="https://github.com/user-attachments/assets/10e5893c-1e25-496e-a9dc-29be3fa9436d">

<p><strong>Explanation:</strong> By adding the <code>IN</code> clause and providing all 7 employee IDs in the query, I retrieved only 6 rows, as one employee had a <code>NULL</code> value in their <code>device_id</code> column.</p>

<hr>

<h3>Task 5 - Retrieving Employee Data in Finance or Sales</h3>
<p><strong>Scenario:</strong> Similar to the last task, my team wants to perform security updates, but this time only for employees in the Sales and Finance departments.</p>

<h4>1st Query Command:</h4>

<img width="631" alt="Screen Shot 2024-11-06 at 1 01 33 AM" src="https://github.com/user-attachments/assets/dde77adf-be8e-4265-b626-25e3907af66c">

<p>Query Results:</p>

<img width="598" alt="Screen Shot 2024-11-06 at 1 02 02 AM" src="https://github.com/user-attachments/assets/edab7ba5-6042-4e5c-a113-1fd14a320257">

<h4>2nd Query Command:</h4>

<img width="608" alt="Screen Shot 2024-11-06 at 1 02 17 AM" src="https://github.com/user-attachments/assets/70dbdbc0-3617-4070-a65f-0419d81ed567">

<p>Query Results:</p>

<img width="630" alt="Screen Shot 2024-11-06 at 1 02 31 AM" src="https://github.com/user-attachments/assets/7f862238-1fcf-4105-8484-55160ed2ec7e">

<p><strong>Explanation:</strong> For this query, I used a subquery within the main query to dynamically fetch employee IDs in the Sales and Finance departments. The subquery <code>SELECT employee_id FROM employees WHERE department = 'Finance' OR department = 'Sales'</code> fetched the IDs, which were then used in the main query on the <code>machines</code> table. This streamlined process ensured accuracy and efficiency.</p>

<hr>

<h3>Task 6 - Retrieving All Employees Not in IT</h3>
<p><strong>Scenario:</strong> My team needs to make a security update on employees who are not in the Information Technology department. To do so, I need to retrieve information on these employees.</p>

<h4>1st Query Command:</h4>

<img width="563" alt="Screen Shot 2024-11-06 at 1 02 47 AM" src="https://github.com/user-attachments/assets/ece3ebbb-4f7c-4abc-822e-ca5a253f9060">

<p>Query Results:</p>

<img width="631" alt="Screen Shot 2024-11-06 at 1 03 04 AM" src="https://github.com/user-attachments/assets/76022006-fb43-45f6-bda1-d497fd0624ce">

<p><strong>Explanation:</strong> This query returns all employees not in the Information Technology department. I selected all data from the <code>employees</code> table, using <code>WHERE NOT</code> to filter out those in IT.</p>

<hr>

<h2>Summary</h2>
<p>In my work, I focused on extracting detailed data regarding login attempts and employee machine usage. Utilizing the <code>log_in_attempts</code> and <code>employees</code> tables, I implemented various filters in my SQL queries. To hone in on the exact data required for each analysis, I employed the <code>AND</code>, <code>OR</code>, and <code>NOT</code> operators, allowing for precise data retrieval. Additionally, I used the <code>LIKE</code> operator with the <code>%</code> wildcard to identify patterns within the data. This approach ensured that I gathered relevant information for each aspect of my investigation.</p>

<h2>Reference</h2>
<p>This Section describes how the tables used for this portfolio activity are organized. The organization database contains the following two tables:</p>

<h3>log_in_attempts</h3>
<p>The <code>log_in_attempts</code> table has the following columns:</p>
<ul>
  <li><strong>event_id:</strong> The identification number assigned to each login event</li>
  <li><strong>username:</strong> The username of the employee</li>
  <li><strong>login_date:</strong> The date the login attempt was recorded</li>
  <li><strong>login_time:</strong> The time the login attempt was recorded</li>
  <li><strong>country:</strong> The country where the login attempt occurred</li>
  <li><strong>ip_address:</strong> The IP address of the employee’s machine</li>
  <li><strong>success:</strong> Indicates the success of the login attempt; <code>FALSE</code> for failed attempts</li>
</ul>
<img width="632" alt="Screen Shot 2024-11-06 at 1 03 23 AM" src="https://github.com/user-attachments/assets/8a008f70-eb22-45bf-a558-427a8294a5b0">

<h3>employees</h3>
<p>The <code>employees</code> table has the following columns:</p>
<ul>
  <li><strong>employee_id:</strong> The identification number assigned to each employee</li>
  <li><strong>device_id:</strong> The identification number assigned to each device used by the employee</li>
  <li><strong>username:</strong> The username of the employee</li>
  <li><strong>department:</strong> The department the employee is in</li>
  <li><strong>office:</strong> The office location of the employee</li>
</ul>
<img width="635" alt="Screen Shot 2024-11-06 at 1 03 52 AM" src="https://github.com/user-attachments/assets/808c2588-adec-4a65-ae12-20dff2ffa3ef">
