# Gym Management System

A console-based gym management application built entirely in Python. Designed to handle the full operational workflow of a gym — from member registration and subscription management to attendance tracking, trainer scheduling, and staff administration.

Built as a solo project to demonstrate object-oriented programming, modular design, and robust input validation in Python.

## Features

**Member Management**

- Register new members with name, mobile number, date of birth, and joining date
- Assign subscription packages (Lite, Basic, Premium, PremiumPlus) at registration
- Update member information and remove members from the system
- Auto-generate secure login credentials using Python's `secrets` module
- Simulate SMS notifications to members upon registration

**Subscription Packages**

| Package | Price | Classes/Week | Private Sessions |
| --- | --- | --- | --- |
| Lite (Weekly) | $10 | 0 | 0 |
| Basic (Weekly) | $25 | 1 | 0 |
| Premium (Monthly) | $100 | 2 | 10 |
| PremiumPlus (Yearly) | $1,150 | 5 | 50 |

**Attendance Tracking**

- Log and view attendance records per member
- Mark attendance by date with present/absent status

**Trainer & Staff Management**

- Add, update, and remove trainers with specialization and working hours
- Add, update, and remove staff members with designation and working hours

**Schedule Management**

- Create fitness program schedules and assign trainers
- Book private sessions for members with a specific trainer and date

**Admin & Member Portals**

- Separate admin and member login flows with password protection
- Members can view their own info, attendance, and subscription details
- Members can change their own password

## Tech Stack

- **Language:** Python 3
- **Libraries:** `dataclasses`, `datetime`, `secrets`, `string` — standard library only, no external dependencies
- **Environment:** Runs in any Python 3 terminal or Google Colab notebook
- **Data storage:** In-memory (runtime only); no database or file I/O required

## Project Structure

The project is organized as a single Python file (or Colab notebook) with clearly separated modules:

```
gym_management_system.py
│
├── Data Models (dataclasses)
│   ├── Subscription   — package name, price, classes, private sessions
│   ├── Member         — personal info, credentials, attendance, subscription
│   ├── Trainer        — name, specialization, working hours
│   ├── Staff          — name, designation, working hours
│   ├── Schedule       — fitness program, assigned trainers, private sessions
│   └── Attendance     — member reference, date, status
│
├── Shared Helpers
│   ├── valid_date()          — validates dd/mm/yyyy input
│   ├── ask_date()            — prompts until a valid date is entered
│   ├── ask_number()          — prompts until a valid number is entered
│   ├── find_member_by_mobile()
│   ├── find_trainer_by_name()
│   ├── find_staff_by_name()
│   ├── generate_random_password()  — uses secrets module
│   └── send_sms()            — demo stub for SMS notifications
│
├── Member Operations
│   ├── add_member(), remove_member(), update_member_information()
│   ├── view_member_information(), view_member_attendance()
│   └── view_subscription_details()
│
├── Trainer & Staff Operations
│   ├── add_trainer(), remove_trainer(), update_trainer()
│   └── add_staff(), remove_staff(), update_staff()
│
├── Schedule & Attendance Operations
│   ├── add_schedule(), assign_trainer_to_schedule()
│   ├── book_private_session(), mark_attendance()
│
└── Menu System
    ├── admin_menu()    — full access to all operations
    └── member_menu()   — self-service portal for members
```

## How to Run

**Option 1 — Google Colab (easiest)**

1. Open the `.ipynb` file in [Google Colab](https://colab.research.google.com)
2. Click **Runtime → Run all**
3. Interact with the menu prompts in the output cell

**Option 2 — Local Python terminal**

1. Make sure Python 3 is installed (`python --version`)
2. Save the notebook as a `.py` file, or copy the code into a `.py` file
3. Run it:

```bash
python gym_management_system.py
```

> No external packages needed — uses Python standard library only.

## Usage

On launch, you are prompted to log in as **Admin** or **Member**.

**Admin login:** uses the admin password defined in the script (`ADMIN_PASSWORD`)

**Member login:** uses the auto-generated username and password sent via SMS on registration

### Example — Registering a new member (Admin)

```
> Select option: Add Member
Full Name: Sarah Ahmed
Mobile Number: 01712345678
Date of Birth (dd/mm/yyyy): 15/03/1995
Date of Joining Gym (dd/mm/yyyy): 01/10/2026

1. Lite (Weekly)       - $10.00
2. Basic (Weekly)      - $25.00
3. Premium (Monthly)   - $100.00
4. PremiumPlus (Yearly)- $1150.00

Choose a package number: 3
Member added successfully with package: Premium (Monthly).
[SMS DEMO to 01712345678] Dear Sarah Ahmed, your username is sarah and password is xT3mK9pL.
```

### Example — Member self-service login

```
> Login as: Member
Username: sarah
Password: xT3mK9pL

1. View my information
2. View my attendance
3. View my subscription
4. Change my password
5. Logout
```

## Future Improvements

- **Persistent storage** — save data to a JSON or SQLite database so records survive between sessions
- **GUI interface** — build a desktop UI using Tkinter or a web front-end using Flask
- **Real SMS integration** — connect to an SMS API (e.g. Twilio) to replace the demo stub
- **Payment tracking** — log and track membership payments alongside subscriptions
- **Search and filter** — allow admins to search members by name, package, or blood group
- **Export reports** — generate attendance or membership reports as CSV or PDF
