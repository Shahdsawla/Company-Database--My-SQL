# Company-Database--My-SQL

Here’s a ready-to-paste **README.md** for GitHub for your `task-1-sql.sql` file (the full CompanyDB schema + sample data).[1]



# CompanyDB SQL 

This repository contains a SQL script that builds a **CompanyDB** relational database schema and inserts sample data for testing.[1]
It creates core company entities (employees, departments, projects) plus relationship tables (works_on, dependents, department locations) and enforces referential integrity using foreign keys.[1]

## Files

- `task-1-sql.sql` — full schema + constraints + sample INSERT/UPDATE statements.[1]

## Database Schema

The script creates the database and these tables:[1]

- `EMPLOYEE`
  - Key fields: `SSN` (PK), `SUPERSSN` (self-FK), `DNO` (FK → `DEPARTMENT.DNUMBER`).[1]
- `DEPARTMENT`
  - Key fields: `DNUMBER` (PK), `MGRSSN` (FK → `EMPLOYEE.SSN`), `MGRSTARTDATE`.[1]
- `DEPT_LOCATIONS`
  - Composite PK: (`DNUMBER`, `DLOCATION`), FK → `DEPARTMENT.DNUMBER` with `ON DELETE CASCADE` and `ON UPDATE CASCADE`.[1]
- `PROJECT`
  - Key fields: `PNUMBER` (PK), `DNUM` (FK → `DEPARTMENT.DNUMBER`).[1]
- `WORKS_ON`
  - Composite PK: (`ESSN`, `PNO`), FKs → `EMPLOYEE.SSN` and `PROJECT.PNUMBER`.[1]
- `DEPENDENT`
  - Composite PK: (`ESSN`, `DEPENDENT_NAME`), FK → `EMPLOYEE.SSN`.[1]

## Sample Data Included

The script inserts example records to help you test queries immediately, including:[1]

- 2 departments: `IT`, `HR`[1]
- 3 employees (with a supervisor relationship via `SUPERSSN`)[1]
- department managers updated after employees are inserted (`UPDATE DEPARTMENT SET MGRSSN = ...`).[1]
- department locations (e.g., Cairo, Alexandria, Giza)[1]
- 2 projects (`HospitalSys`, `HRPortal`)[1]
- works-on assignments with hours[1]
- dependents for employees[1]

## How to Run

### Option A: MySQL Workbench 
1. Open your MySQL server.
2. Run:

```sql
SOURCE task-1-sql.sql;
```


## Notes

- Because `EMPLOYEE.SUPERSSN` references `EMPLOYEE.SSN` and `DEPARTMENT.MGRSSN` references `EMPLOYEE.SSN`, the script correctly inserts departments with `MGRSSN = NULL` first, inserts employees, then updates managers.[1]
- `DEPT_LOCATIONS` is configured to cascade changes from `DEPARTMENT` (`ON DELETE`/`ON UPDATE CASCADE`).[1]

