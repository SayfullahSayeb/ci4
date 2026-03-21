# CodeIgniter 4 - My Reusable Master Template

This is my personal master template with Shield Auth + SQLite.

### Setup Commands
```bash
composer create-project codeigniter4/appstarter project-root
cd project-root
composer require codeigniter4/shield          # install shield
php spark shield:setup                        # shield setup
rm -rf tests                                  # remove tests folder
mv env .env                                   # rename environment file
```
# Database Setup (SQLite)
Edit .env file and add:
```
database.default.DBDriver = SQLite3
database.default.database = writable/database.sqlite3
database.default.DBPrefix = 
```
```
php spark migrate --all                       # run migrations
```
```
php spark shield:user create                  # create first user
php spark shield:user addgroup your_username superadmin   # make user superadmin
```
# Remove `index.php` from URL
Edit `app/Config/App.php` → set `$indexPage = '';`
Add `.htaccess` in root

### How to Start New Project from Master
```bash
git clone https://github.com/yourusername/ci4-master.git my-new-project
cd my-new-project
composer install
php spark migrate --all
php spark shield:user create
php spark shield:user addgroup your_username superadmin
php spark serve
```
### Project Structure & How to Work

All controller logic → `app/Controllers/MainController.php`
All view files → `app/Views/pages/`
Shared layout → `app/Views/layout.php`
Assets (css, js, images) → `public/assets/`

Link assets like this:
`<link rel="stylesheet" href="<?= base_url('assets/css/style.css') ?>">`

### How to Add New Page

1. Add method in `MainController.php`
2. Create view file in `app/Views/pages/`
3. Add route in `app/Config/Routes.php`

### Development Commands
```bash
php spark serve                    # run local server
composer install --no-dev          # production build
php spark migrate --all            # run migrations
php spark cache:clear              # clear cache
```
### Notes

- This master uses SQLite by default (easy cloning)
- Shield authentication is ready
- Use MainController.php for all page logic
- Keep BaseController.php as it is
- All custom work should be done in MainController.php and Views/pages/

Last Updated: March 2026
