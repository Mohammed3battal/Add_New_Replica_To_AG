## Script: Add New Replica to Availability Group Without Password

**Description**:
This script automates the process of adding a new SQL Server replica (e.g., DR or new secondary) to an existing Always On Availability Group without requiring a password. It uses Windows-authenticated SQL service accounts or built-in accounts like NT SERVICE\MSSQLSERVER. The script covers endpoint creation, permission grants, health session configuration, and replica joining — all using SQLCMD mode.
**Steps Performed**:
1.Grants CONNECT permission on Hadr_endpoint to SQL Server service accounts on the Primary, Secondary, and DR nodes.
2.Creates and starts Hadr_endpoint on the new replica node if it doesn’t already exist.
3.Grants CONNECT permission to the SQL service account on the new replica.
4.Enables the AlwaysOn_health Extended Events session on the new replica.
5.Adds the new replica from the Primary node using ALTER AVAILABILITY GROUP ... ADD REPLICA.
6.Joins the new replica to the AG and grants CREATE ANY DATABASE permission to allow automatic seeding.

**Notes**:
- Execute this script in **SQLCMD Mode**.
- Replace the following placeholders before running:
*[SQL Service account]
*[AG_Name]
*Node name that you need add it
- Default port is `5022` — change if needed.
- Designed for SQL Server 2016 or later.

**Requirements**:
- Always On must be enabled and configured.
- SQL Service accounts must match across nodes.
- Run under `sysadmin` privileges on all participating nodes.
