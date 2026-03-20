# CodeIgniter 4 - Modular Master Template

This is my personal reusable master template for CodeIgniter 4 projects.  
It uses **HMVC Modular Structure** to keep code clean, organized, and easy to maintain across multiple projects.

---

## 1. Initial Project Setup

### Step 1: Create Fresh Project

```bash
composer create-project codeigniter4/appstarter project-root
cd project-root
```

### Step 2: Clean & Prepare

```bash
# Remove unnecessary tests folder
rm -rf tests

# Copy environment file
cp env .env
```

### Step 3: Install Dependencies

```bash
# For development
composer install

# For production (smaller size)
composer install --no-dev --optimize-autoloader
```

### Step 4: Run Server (Testing)

```bash
php spark serve
```

---

## 2. Authentication (Shield)

### Install Shield

```bash
composer require codeigniter4/shield
```

### Setup Shield

```bash
php spark shield:setup
```

### Configure Database in `.env`

```env
database.default.hostname = localhost
database.default.database = your_database_name    # Change this
database.default.username = root
database.default.password =
database.default.DBDriver = MySQLi
database.default.port = 3306
```

### Run Migrations

```bash
php spark migrate --all
```

### Create First Super Admin User

```bash
php spark shield:user create
```

Then add superadmin group:

```bash
php spark shield:user addgroup your_username superadmin
```

---

## 3. Modular HMVC Structure (Our Main Architecture)

We use Modular HMVC pattern so each feature lives in its own folder.

### Folder Structure

```text
app/
├── Modules/
│   ├── Dashboard/
│   │   ├── Controller.php
│   │   └── Views/
│   │       └── index.php
│   ├── Admin/
│   │   ├── Controller.php
│   │   └── Views/
│   │       └── index.php
│   └── Products/
│       ├── Controller.php
│       └── Views/
│           └── index.php
├── Config/
│   └── Routes.php
└── Views/
    └── layout.php
```

### How to Add a New Module (Future Pages)

1. Create a new folder inside `app/Modules/` (e.g. Blog)  
2. Create `Controller.php` and `Views/` folder inside it  
3. Add one line in `app/Config/Routes.php`  

### Example for "Blog" module:

```php
$routes->get('blog', 'Modules\Blog\Controller::index');
```

---

## 4. How to Start a New Project (From This Master)

### Clone this master repo:

```bash
git clone your-master-repo.git my-new-project
cd my-new-project
```

### Install dependencies:

```bash
composer install
```

### Copy environment file:

```bash
cp .env.example .env
```

### Update `.env` with new database name

### Run migrations:

```bash
php spark migrate --all
```

### Create your first superadmin user:

```bash
php spark shield:user create
php spark shield:user addgroup your_username superadmin
```

---

## 5. Development Commands

```bash
php spark serve #Run local development server
composer install --no-dev #Production build (smaller size)
composer update #Update dependencies
php spark migrate --all #Run all migrations
php spark cache:clear #Clear cache
```

---

## Notes

- All custom code should go `inside app/Modules/`
- Shared layout file is located at `app/Views/layout.php`
- Shield authentication is fully integrated and ready to use
- This modular structure is designed for easy cloning, maintenance, and long-term scalability
- Avoid putting custom code directly in `app/Controllers/` or `app/Views/` — always use Modules

# Made with ❤️ for fast and clean development
