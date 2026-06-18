# Database Design

## Employee

Stores employee master information.

Fields:

* id
* employeeCode
* firstName
* lastName
* email
* department
* designation
* country
* currency
* createdAt
* updatedAt

Indexes:

* employeeCode
* email
* department
* country

---

## Salary

Stores current salary information.

Fields:

* id
* employeeId
* baseSalary
* bonus
* effectiveDate
* isCurrent
* createdAt

Relationship:
Employee (1) -> (N) Salary

---

## SalaryHistory

Stores salary change audit records.

Fields:

* id
* employeeId
* oldSalary
* newSalary
* reason
* changedAt

Purpose:
Maintain a complete audit trail for compensation changes.

---

## Relationships

Employee
|
+---- Salary
|
+---- SalaryHistory
