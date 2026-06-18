# API Contracts

## Employees

GET /employees

Query Params:

* page
* pageSize
* search
* department
* country

Response:
{
data: Employee[],
total: number,
page: number
}

---

GET /employees/:id

Response:
{
employee: Employee,
currentSalary: Salary
}

---

## Salaries

PUT /employees/:id/salary

Request:
{
salary: number,
effectiveDate: string,
reason: string
}

Response:
{
success: true
}

---

GET /employees/:id/salary-history

Response:
{
history: SalaryHistory[]
}

---

## Analytics

GET /analytics/overview

GET /analytics/country

GET /analytics/department

---

## Insights

POST /insights/query

Request:
{
question: string
}

Response:
{
answer: string
}
