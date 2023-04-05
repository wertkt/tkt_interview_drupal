# TKT DRUPAL INTERVIEW

## Prerequisites
Make sure you have Composer installed and running on your machine. See https://getcomposer.org/doc/00-intro.md to install Composer

## Installation
Mount a local LAMP environment using any tool you like with php > 8.1

The webhost should point to tkt_interview_drupal/web/index.php (Drupal is installed in the `web` directory)

A MySQL database shall be created and named `tkt_interview` with a user and a password

Once your server is running, run the following commands from the tkt_interview_drupal/ repository:
- `composer install` to fetch all php dependencies
- run `vendor/bin/drush si tkt --site-name="TKT Drupal" --account-pass="admin" --db-url=mysql://{user}:{password}@localhost:{port}/tkt_interview` where `{user}` is the name of your DB user, `{password}` is the password associated to you DB user and `{port}` is the port used by the DB server (usually 3306)
- Head to the URL defined in your webhost. You should have a fully installed Drupal.


## TASKS
IMPORTANT: Write all your code in the `web/modules/custom/tkt_interview` directory. The `tkt_interview` module is enabled already.

The admin credentials are `admin` / `admin`
### RULES
The test shall take approx. 1h

- Apply the PHP and Drupal best practices.
- Do not install or enable any other module that then ones already there
- Do not use the `views` module
- If you have trouble understanding a step, you may contact us to clarify it
- If you are not able to finish the test, send everything "as it is"


### Step 1: Create a content type
Create a content type that represents a Book

A Book is defined by:
- a title (mandatory)
- a description
- an author name (mandatory)

**Optional** A book can have a price and a unique identifier (SKU)

**Tip** Once the content type is created, you may use the `devel_generate` module to generate lots of contents.

### Step 2: Retrieve contents and create a permission
Create a custom route and a controller to display the titles of the published Books

Books must be ordered by ascending titles.

Create a `manage books` custom permission. Your custom route shall be accessible only to users having this permission

### Step 3: Add a menu entry and a permission
Add a menu entry pointing to this route in the administration toolbar.

The menu entry shall be a sub-entry of the "System" (`/admin/config/system`) menu entry.


### Step 4: Implement a hook
Implement the `hook_preprocess_page_title()` hook to alter every page title.

When the user has the `manage books` permission, every page title shall have the CSS class `book-title-custom`.

**Tip** If your changes do not appear at once, use the `vendor/bin/drush cr` command to flush the Drupal cache

### Step 5: Create a custom library
Create a custom library to include a custom CSS file from your module

This CSS file shall contain the style to turn the text color of elements having the `book-title-custom` class to red.

**Tip** Be careful with the cache ;-)
