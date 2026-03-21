# CodeIgniter 4 with Shield Auth + SQLite.

### What I did,
```bash
composer create-project codeigniter4/appstarter project-root
cd project-root
mv env .env                                   # rename environment file
composer require codeigniter4/shield          # install shield
php spark shield:setup                        # shield setup
rm -rf tests                                  # remove tests folder
```
### Database Setup (SQLite)
Edit .env file and add:
```
database.default.DBDriver = SQLite3
database.default.database = database.db
database.default.DBPrefix = 
```
for sync
```bash
php spark migrate --all                       # run migrations
```
### Removed `index.php` from URL
Edit `app/Config/App.php` → set `$indexPage = '';`
Add `.htaccess` in root

### How to Start New Project from Master
```bash
git clone https://github.com/SayfullahSayeb/ci4.git
cd ci4
php spark cache:clear
composer install
mv env .env                                   # rename environment file
php spark migrate --all
php spark serve
```

### For add user
```bash
php spark shield:user create
php spark shield:user addgroup your_username superadmin
php spark shield:user list
```
### Project Structure & How to Work

All controller logic → `app/Controllers/` or `app/Controllers/MainController.php` <br>
All view files → `app/Views/pages/`<br>
Add route in `app/Config/Routes.php` <br>
Shared layout → `app/Views/layout.php`<br>
Assets (css, js, images) → `public/assets/`<br>

Link assets like this:
`<link rel="stylesheet" href="<?= base_url('assets/css/style.css') ?>">`

### Development Commands
```bash
composer update                    # Update dependencies
php spark migrate --all            # run migrations
php spark cache:clear              # clear cache
php spark serve                    # run local server
composer install --no-dev          # production build
```
### Notes

- This master uses SQLite by default
- Shared layout file is located at `app/Views/layout.php`
- Shield authentication is fully integrated and ready to use

Last Updated: March 2026
