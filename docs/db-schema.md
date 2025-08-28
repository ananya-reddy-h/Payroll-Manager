# Payroll Management Suite — Database Schema

Database: MongoDB  
Collections: Employees, Payrolls, Payslips, Disputes, Notifications

---

## 1. employees
| Field         | Type      | Description |
|--------------|----------|-------------|
| _id         | ObjectId | Unique employee ID |
| name        | String   | Employee's full name |
| email       | String   | Login email |
| password    | String   | Hashed password |
| role        | String   | "employee", "admin", "hr" |
| department  | String   | Department name |
| salary      | Number   | Base salary |
| allowances  | Number   | Allowances |
| deductions  | Number   | Deductions |
| createdAt   | Date     | Auto |
| updatedAt   | Date     | Auto |

---

## 2. payrolls
| Field        | Type      | Description |
|-------------|----------|-------------|
| _id        | ObjectId | Unique payroll ID |
| employeeId | ObjectId | FK → employees._id |
| month      | String   | Month of payroll |
| grossPay   | Number   | Basic + Allowances |
| deductions | Number   | Total deductions |
| tax        | Number   | Tax deducted |
| netPay     | Number   | Final salary |
| status     | String   | "generated", "pending" |
| createdAt  | Date     | Auto |

---

## 3. payslips
| Field        | Type      | Description |
|-------------|----------|-------------|
| _id        | ObjectId | Unique slip ID |
| employeeId | ObjectId | FK → employees._id |
| payrollId  | ObjectId | FK → payrolls._id |
| pdfUrl     | String   | URL of stored payslip |
| qrCode     | String   | Verification QR code |
| createdAt  | Date     | Auto |

---

## 4. disputes
| Field       | Type      | Description |
|------------|----------|-------------|
| _id       | ObjectId | Unique dispute ID |
| employeeId| ObjectId | FK → employees._id |
| payrollId | ObjectId | FK → payrolls._id |
| issue     | String   | Issue description |
| status    | String   | "open", "in-progress", "resolved" |
| comments  | [String] | Admin/HR responses |
| createdAt | Date     | Auto |

---

## 5. notifications
| Field      | Type      | Description |
|-----------|----------|-------------|
| _id      | ObjectId | Unique notification ID |
| userId   | ObjectId | FK → employees._id |
| type     | String   | "email" / "popup" |
| message  | String   | Notification text |
| status   | String   | "unread", "read" |
| createdAt| Date     | Auto |