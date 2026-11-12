# DRRM Compliance System

**Disaster Risk Reduction and Management (DRRM) Compliance System** for schools — a Laravel web application that lets SDO/school personnel track fire safety compliance, evacuation monitoring, incidents, and comprehensive school safety in one place.

![Tech](https://img.shields.io/badge/Laravel-12-red) ![PHP](https://img.shields.io/badge/PHP-%3E%3D8.2-blue) ![DB](https://img.shields.io/badge/MySQL/MariaDB-database-orange)

> This is the independent copy of the system for this repository. The original team project lives at [DRRM-Compliance/drrm-compliance-system](https://github.com/DRRM-Compliance/drrm-compliance-system). You are free to change anything here.

---

## Modules

| Module | What it does |
|---|---|
| **Fire Safety** | Buildings, rooms, fire extinguishers (pressure & status tracking), alarm systems, evacuation plans, inspection checklists, printable full-school reports, evacuation map layout editor |
| **Evacuation Monitoring (Typhoon/Flood)** | Evacuation centers, family check-in/check-out, family members with vulnerability tags (PWD, senior, pregnant, lactating, under-5), needs monitoring |
| **Incident Checklist** | Incident calendar (incident & compliance entries with attachments), incident types/statuses, daily checklists, reporting dashboard |
| **Comprehensive School Safety** | School assessments with scored questionnaires, facilities, students & pathway tracking, safety-index reports |
| **Drill Monitoring** | Evacuation drill scheduling, logging, inspection tool, print reports |
| **Hazard Mapping** | Hazard identification & mapping (under development) |
| **Damage Reports** | Damage reporting of facilities and resources (under development) |
| **Inventory Storage** | Disaster-preparedness gear and equipment inventory |
| **Admin tools** | User & role management (admin/contributor), module access assignment, unified school directory, announcements, activity logs, database backup download |

## Tech Stack

- **Backend:** Laravel 12 (PHP 8.2+), MySQL / MariaDB
- **Frontend:** Blade templates, Bootstrap 5, Tailwind CSS, Vite, SweetAlert2, Font Awesome
- **Auth:** Laravel UI (login/register with e-mail verification code)

## Requirements

- PHP >= 8.2 (with `pdo_mysql`, `mbstring`, `openssl`, `fileinfo` extensions)
- Composer *(not installed? use the bundled `composer.phar` — see below)*
- Node.js >= 18 + npm (only needed to rebuild front-end assets)
- MySQL or MariaDB (XAMPP works fine)

## Setup (XAMPP / Windows quick way)

1. Install XAMPP and start **Apache** + **MySQL**.
2. Copy this project to `C:\xampp\htdocs\drrmc-compliance` (or anywhere).
3. Double-click **`autostart.bat`** — it starts XAMPP services and the Laravel dev server on `http://127.0.0.1:8000`.

The first time you still need the manual steps below (`.env`, database, packages).

## Setup (manual)

```bash
# 1. Install PHP dependencies
composer install
#    ...or if you don't have Composer installed:
php composer.phar install

# 2. Environment file
cp .env.example .env          # Windows: copy .env.example .env
php artisan key:generate

# 3. Database
#    - create an empty MySQL database named `drrmcompliance`
#    - then EITHER import the full copy with data:
mysql -u root -p drrmcompliance < drrmcompliance.sql
#    ...or start blank (runs migrations + seeders):
php artisan migrate --seed

# 4. Front-end assets (optional — only when changing CSS/JS)
npm install
npm run dev        # dev server   |   npm run build   # production bundle

# 5. Run
php artisan serve
```

Open **http://127.0.0.1:8000** and log in.

## Default Accounts

| Role | E-mail | Password |
|---|---|---|
| Admin (seeder) | `adankristopher.dumpit@gmail.com` | `password123` |

*Imported via `drrmcompliance.sql`? The database already contains its own users — ask the previous admin for credentials, or reset any password directly in the `users` table (Laravel bcrypt hash).*

> ⚠️ Change the default admin password before using this in production.

## Project Structure (key folders)

```
app/Http/Controllers/   FireSafety, Typhoon, Incident, ComprehensiveSchoolSafety,
                        DrillMonitoring, InventoryStorage, HazardMapping, Dashboard, ...
app/Models/             Eloquent models for every module
database/migrations/    Full schema history (100+ migrations)
database/seeders/       AdminUserSeeder, SystemConfigurationSeeder
resources/views/        Blade views per module (fire-safety/, typhoon/, incidents/, ...)
routes/web.php          All application routes
drrmcompliance.sql      Full MySQL dump (schema + data) for quick setup
autostart.bat           One-click launcher for XAMPP on Windows
DRRM System Development Reference/   Installation guide, user manual, tasks
encoded_schools_inspection_record/   Sample fire safety print reports (PDF)
```

## Database

The quickest way to get the exact working system is importing **`drrmcompliance.sql`** into an empty `drrmcompliance` database (it includes all schools, users, fire-safety records and the migration history). Use phpMyAdmin (Import tab) or the `mysql` command shown above.

## Tests

```bash
php artisan test
```

## Credits

Based on the team project [DRRM-Compliance/drrm-compliance-system](https://github.com/DRRM-Compliance/drrm-compliance-system) (DepEd SDO Olongapo City DRRM). Built with the [Laravel framework](https://laravel.com).
