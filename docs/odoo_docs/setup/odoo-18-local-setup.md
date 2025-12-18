# Odoo 18 – Local Development Setup Guide

This document explains how to set up **Odoo 18** on a local machine using **Python 3.10**, **PostgreSQL**, and a **virtual environment**.

---

## Prerequisites

Ensure the following are installed on your system:

- Python **3.10**
- PostgreSQL (latest stable version)
- Git
- VS Code (recommended)
- pip (comes with Python)

---

## Step 1: Install Required Python Packages

```bash
pip install wheel setuptools
pip install psycopg2-binary lxml babel pytz pillow werkzeug

## Step 2: Clone Odoo Source Code

### Clone Odoo 18.0 (Recommended)

Use the following command to clone the official Odoo repository with the **18.0** branch:

```bash
git clone https://github.com/odoo/odoo.git --branch 18.0 C:\odoo18

### OR Clone the Default Branch

If you want to clone the default branch instead, use the following commands:

```bash
git clone https://github.com/odoo/odoo.git
cd odoo

## Step 3: Create Python Virtual Environment

Navigate to the Odoo directory:

```bash
cd C:\odoo18

## Create Python Virtual Environment

Create a virtual environment inside the Odoo project directory:

```bash
python -m venv myenv
> This creates a folder named `myenv` inside the Odoo project.

---

## Activate the Virtual Environment

### Windows
```bash
myenv\Scripts\activate
> This creates a folder named `myenv` inside the Odoo project.

---

## Activate the Virtual Environment

### Windows
```bash
myenv\Scripts\activate

### Linux / macOS – Activate Virtual Environment

```bash
source myenv/bin/activate

## Step 4: Install Python Dependencies

Install the required Python packages:

```bash
pip install wheel
pip install psycopg2-binary
pip install -r requirements.txt

## Step 5: PostgreSQL Setup

### Login to PostgreSQL
Open your terminal and log in to PostgreSQL as the `postgres` user:

```bash
psql -U postgres

## Create Odoo PostgreSQL User

Run the following SQL command in your PostgreSQL prompt to create a dedicated user for Odoo:

```sql
CREATE USER odoo WITH SUPERUSER PASSWORD 'odoo';

## Create Odoo Database

Run the following SQL command in your PostgreSQL prompt to create the Odoo database and assign ownership to the `odoo` user:

```sql
CREATE DATABASE odoo_db OWNER odoo;

## Step 6: Create PostgreSQL User via pgAdmin (GUI Method)

Follow these steps to create the Odoo database user using pgAdmin:

1. **Open pgAdmin**
2. **Connect** to your PostgreSQL server
3. Navigate to **Object → Create → Login/Group Role**
4. In the **General** tab, enter:
   - **Role Name:** `odoo`
5. Switch to the **Definition** tab:
   - Set **Password:** `odoo`
6. Go to the **Privileges** tab:
   - ✅ **Can login?** → Yes  
   - ✅ **Create database?** → Yes
7. Click **Save**

## Step 7: Create Odoo Configuration File

1. Navigate to the **Odoo root folder** (the directory containing `odoo-bin`).
2. Create a new file named: `odoo.conf`

## Odoo Configuration File (`odoo.conf`)

Create a file named `odoo.conf` in your Odoo root directory and include the following configuration:

```ini
[options]
admin_passwd = admin
db_host = localhost
db_port = 5432
db_user = odoo
db_password = odoo
db_name = odoo_db
addons_path = addons

## Step 8: Run the Odoo Server

### Initial Database Initialization

The first time you start Odoo, initialize the base database using:

```bash
python odoo-bin --config=odoo.conf --init base

This command sets up the core Odoo database structure.

## Normal Run Command

After the initial setup, start the Odoo server with:

```bash
python odoo-bin --config=odoo.conf

## Step 9: Access Odoo in Browser

Open your web browser and navigate to:

[http://localhost:8069](http://localhost:8069)

### Default Login Credentials

- **Email:** `admin`  
- **Password:** `admin`