# 🚌 Cloud Based Bus Pass System

A web-based application that allows students to **book**, **manage**, **renew**, and **suspend** their bus passes online — eliminating the need for manual, in-person registration.

---

## 📋 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Installation & Setup](#installation--setup)
- [Running the Project](#running-the-project)
- [Pages Overview](#pages-overview)

---

## 📖 About the Project

The **Cloud Based Bus Pass System** is developed to simplify bus pass registration and renewal for students travelling to/from **Chandigarh University, Mohali**. 

In the traditional system, students had to physically visit an office on a specific date and time — missing the window meant missing the renewal. This online system lets students:

- Register and book a pass anytime, from anywhere
- Pay online and receive a digital pass
- Renew their pass before expiry
- View or print their pass details
- Suspend a lost/unused pass

---

## ✨ Features

- 🎫 **Online Pass Booking** — Fill a form, choose destination, proceed to checkout
- 🔁 **Pass Renewal** — Extend validity date online without standing in line
- 👁️ **Pass Management** — Look up pass details using Pass ID + Password
- 🚫 **Pass Suspension** — Suspend an active pass instantly
- 🖨️ **Print Pass** — Print-friendly pass view (hides UI chrome)
- 🗺️ **Destinations** — View all covered routes (Delhi, Agra, Mathura, Vrindavan, Barsana, Chaumuhan)
- 🚌 **Bus Details** — Browse bus numbers, timings, source & destination for all routes
- 📱 **Responsive Design** — Works on desktop and mobile

---

## 🛠️ Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Frontend   | HTML5, CSS3, Bootstrap 4          |
| Styling    | Custom CSS (`style.css`, `enhance.css`) |
| Backend    | PHP (procedural)                  |
| Database   | MySQL                             |
| Server     | Apache (via XAMPP)                |
| Libraries  | jQuery, AOS.js, Owl Carousel, Flaticon |

---

## 📁 Project Structure

```
Cloud-Based-Buss-Pass-System/
│
├── index.html          # Home page — hero, stats bar, destinations
├── about.html          # About page — company info & founder
├── contact.html        # Contact page — address & info
├── bus_details.html    # Bus route details & timings
│
├── book.php            # Pass booking form (POST → billing.php)
├── billing.php         # Billing/payment step
├── invoice.php         # Invoice generation after payment
├── manage.php          # Look up & manage a pass by ID + password
├── manage2.php         # Wrong password redirect page
├── renew.php           # Pass renewal handler
├── suspend.php         # Pass suspension handler
├── connection.php      # MySQL database connection
│
├── css/
│   ├── style.css       # Main stylesheet
│   ├── enhance.css     # UI enhancement layer (modern design)
│   └── bootstrap.min.css
│
├── js/
│   ├── main.js
│   └── jquery-3.3.1.min.js
│
├── images/             # All page images
└── fonts/              # Icon fonts (icomoon, flaticon)
```

---

## 🗄️ Database Schema

**Database name:** `travel`

### Table: `pass`

| Column     | Type         | Description                  |
|------------|--------------|------------------------------|
| `id`       | INT (PK, AI) | Unique Pass ID               |
| `name`     | VARCHAR      | Student's full name          |
| `email`    | VARCHAR      | Student's email address      |
| `contact`  | VARCHAR      | Mobile number                |
| `password` | VARCHAR      | Pass access password         |
| `date`     | DATE         | Pass validity date           |
| `dest`     | VARCHAR      | Destination (route)          |
| `paid`     | VARCHAR/INT  | Amount paid                  |

### Table: `destination`

| Column | Type    | Description       |
|--------|---------|-------------------|
| `name` | VARCHAR | Destination name  |

---

## ⚙️ Installation & Setup

### Prerequisites

Make sure you have the following installed:

- ✅ [XAMPP](https://www.apachefriends.org/) (includes Apache + MySQL + PHP)
- ✅ A modern web browser (Chrome, Firefox, Edge)
- ✅ Git (optional, for cloning)

---

### Step 1 — Clone or Download the Project

**Option A — Clone via Git:**
```bash
git clone https://github.com/22bcg80001/Cloud-Based-Bus-Pass-System.git
```

**Option B — Download ZIP:**
- Click the green **Code** button on GitHub → **Download ZIP**
- Extract the folder

---

### Step 2 — Place Project in XAMPP Directory

Move the project folder into your XAMPP `htdocs` directory:

```
# Default XAMPP paths:
C:\xampp\htdocs\        ← Windows (C Drive)
D:\xampp\htdocs\        ← Windows (D Drive)
/opt/lampp/htdocs/      ← Linux
/Applications/XAMPP/htdocs/  ← macOS
```

Your final path should look like:
```
C:\xampp\htdocs\Cloud-Based-Buss-Pass-System\
```

---

### Step 3 — Start XAMPP as Administrator

1. **Right-click** XAMPP Control Panel → **Run as administrator**
2. Click **Start** next to **Apache**
3. Click **Start** next to **MySQL**
4. Both should turn **green** (Running)

> ⚠️ **Port conflict?** If Apache fails to start, another application may be using port 80. In XAMPP → Apache → **Config** → `httpd.conf`, change `Listen 80` to `Listen 8080` and try again.

---

### Step 4 — Create the Database

1. Open your browser and go to:
   ```
   http://localhost/phpmyadmin
   ```
2. Click **New** in the left panel
3. Create a database named exactly:
   ```
   travel
   ```
4. Select the `travel` database, then click the **SQL** tab
5. Paste and run the following SQL:

```sql
-- Create destination table
CREATE TABLE destination (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

-- Insert destinations
INSERT INTO destination (name) VALUES
  ('Delhi'),
  ('Agra'),
  ('Mathura'),
  ('Vrindavan'),
  ('Barsana'),
  ('Chaumuhan');

-- Create pass table
CREATE TABLE pass (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(150) NOT NULL,
  contact VARCHAR(15) NOT NULL,
  password VARCHAR(100) NOT NULL,
  date DATE NOT NULL,
  dest VARCHAR(100) NOT NULL,
  paid VARCHAR(50)
);
```

---

### Step 5 — Configure Database Connection

Open `connection.php` and verify the credentials match your XAMPP MySQL setup:

```php
<?php
  $servername = "localhost";
  $username   = "root";
  $password   = "";        // Default XAMPP MySQL password is empty
  $conn = mysql_connect($servername, $username, $password);
  $sql  = mysql_select_db('travel', $conn);
?>
```

> ⚠️ **Note:** The project uses the deprecated `mysql_*` functions. These work with **PHP 5.x**. If you're on **PHP 7+** (XAMPP 8.x), you may need to use `mysqli_*` functions or enable the `php_mysql` extension.

---

### Step 6 — Run the Project

Open your browser and navigate to:

```
http://localhost/Cloud-Based-Buss-Pass-System/index.html
```

Or if you changed Apache to port 8080:
```
http://localhost:8080/Cloud-Based-Buss-Pass-System/index.html
```

---

## 🗺️ Pages Overview

| Page               | URL                    | Description                            |
|--------------------|------------------------|----------------------------------------|
| Home               | `index.html`           | Landing page with hero & destinations  |
| About              | `about.html`           | Company info & founder                 |
| Contact            | `contact.html`         | Contact info & university location     |
| Bus Details        | `bus_details.html`     | Route timings for all destinations     |
| Book Pass          | `book.php`             | Pass booking form                      |
| Manage Pass        | `manage.php`           | Look up pass by ID + password          |

---

## 📄 License

This project was developed as an academic project at **Chandigarh University, Mohali**.  
© 2024 All rights reserved.
