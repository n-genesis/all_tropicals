# B2B Tropical Plant Wholesale CMS

A custom-engineered **CodeIgniter 4** Content Management System designed specifically for wholesale agricultural and tropical tree production facilities (B2B). This platform bypasses standard consumer shopping carts to focus entirely on structural specifications, live inventory sheets synchronizations, high-efficiency bulk sourcing quotes, and industrial field logs.

## 🚀 Key Architectural Features
- **Non-Transactional Catalog:** Data-dense spec matrices tailored for landscape contractors, property developers, and plant brokers.
- **Excel Availability Sync Engine:** Backed by `phpoffice/phpspreadsheet` to instantly parse and update on-site stock indices from internal greenhouse spreadsheets.
- **Advanced Sourcing Pipelines:** Dedicated multi-step lead capture infrastructure processing structural height parameters, logistics deadlines, and delivery zip codes.
- **Field Logs & Innovation Stream:** Authoritative editorial framework mapping crop development cycles, biosecurity protocols, and regional adaptation metrics.

---

## 📂 System Map & Directory Structure

```markdown
app/
├── Config/
│   └── Routes.php             # Custom routing rules for front-end & admin panel
├── Controllers/
│   ├── BaseController.php     # Global configurations (shared styles, themes)
│   ├── Home.php               # Public Landing page controller
│   ├── Products.php           # Handles available plant listings (Non-transactional)
│   ├── Services.php           # Service information articles & business resources
│   ├── Inquiries.php          # Processes Bulk Orders & Free Business Quotes
│   ├── Insights.php           # Public blog articles & architectural resources
│   ├── Newsletter.php         # Public subscription endpoint
│   └── Admin/                 # Secure CMS Dashboard Controllers
│       ├── Dashboard.php      # Main admin panel homepage
│       ├── Catalog.php        # Manage plant inventory & sync availability sheets
│       ├── Catalog.php        # Manage plant inventory & sync availability sheets
│       ├── Leads.php          # Review bulk orders and custom quote submissions
│       ├── Articles.php       # WYSIWYG management for insights & field logs
│       └── Subscribers.php    # Manage newsletter mailing lists & export CSVs
├── Models/
│   ├── ProductModel.php       # Interacts with `products` table
│   ├── ServiceModel.php       # Interacts with `services` (Insights posts)
│   ├── InquiryModel.php       # Interacts with `inquiries` (Quotes & Bulk Orders)
│   ├── ArticleModel.php       # Interacts with `articles` (Insights posts)
│   └── SubscriberModel.php    # Interacts with `subscribers` (Newsletter list)
├── Views/
│   ├── layouts/               # Shared structural files
│   │   ├── main.php           # Public base layout wrapper (Bootstrap 5 template)
│   │   └── admin.php          # Protected admin panel layout wrapper
│   ├── public/                # Public facing templates
│   │   ├── home.php           # Home page template
│   │   ├── products/          # Plant catalog templates
│   │   │   ├── index.php      # Table view list with filters & excel download triggers
│   │   │   └── view.php       # Specific product page with Sourcing Inquiry form
│   │   ├── insights/          # Blog / Field Log templates
│   │   │   ├── index.php      # Resource feed grid layout
│   │   │   └── read.php       # Full post layout with integrated slider/carousel
│   │   └── contact.php        # Contact page layout with B2B validation logic
│   └── admin/                 # CMS Backend UI Templates
│       ├── login.php          # Admin secure portal login screen
│       ├── dashboard.php      # Metrics panel (Recent inquiries count, graph)
│       ├── catalog/           # Add/Edit products and toggle availability status
│       ├── leads/             # View, search, and change status of B2B entries
│       ├── articles/          # Content creation engine for blog entries
│       └── subscribers/       # List of emails with option to export .csv files
```

---

## 🔀 Core Production Routes (`Config/Routes.php`)

```php
// ==========================================
// Public Front-End Routes
// ==========================================
$routes->get('/', 'Home::index');
$routes->get('contact', 'Home::contact');

// Non-transactional catalog routes
$routes->get('inventory', 'Products::index');
$routes->get('inventory/(:segment)', 'Products::view/$1');

// Leads Processing Endpoints
$routes->post('inquiries/submit', 'Inquiries::submit');
$routes->post('newsletter/subscribe', 'Newsletter::subscribe');

// Technical Briefings / Insights Routes
$routes->get('insights', 'Insights::index');
$routes->get('insights/(:segment)', 'Insights::read/$1');

// ==========================================
// Private Admin CMS Routes (Protected by Auth Filter)
// ==========================================
$routes->group('admin', ['filter' => 'auth'], function($routes) {
    $routes->get('/', 'Admin\Dashboard::index');
    
    // Catalog Management 
    $routes->get('catalog', 'Admin\Catalog::index');
    $routes->post('catalog/sync', 'Admin\Catalog::syncExcel'); // Parse incoming spreadsheet updates
    
    // B2B Lead Pipelines
    $routes->get('leads', 'Admin\Leads::index');
    $routes->get('leads/view/(:num)', 'Admin\Leads::view/$1');
    
    // Articles & Newsletters
    $routes->resource('articles', ['controller' => 'Admin\Articles']);
    $routes->get('subscribers', 'Admin\Subscribers::index');
    $routes->get('subscribers/export', 'Admin\Subscribers::exportCSV');
});

```

---

## ⚙️ Quick-Start Deployment Sequence

### 1. Initialize Dependencies
Install all package requirements, including core data structures and spreadsheet utilities:
```bash
composer install
```

### 2. Configure Environment Environmentals
Duplicate the boot template file and configure your live parameters database string setup inside the custom root directory:
```bash
cp env .env
```
Ensure your configuration fields align:
```ini
CI_ENVIRONMENT = development
database.default.hostname = localhost
database.default.database = ngen_all_tropicals_db
database.default.username = root
database.default.password = your_password
```

### 3. Run Relational Database Migrations
Execute CodeIgniter's migration pipeline to stand up the unified `products`, `inquiries`, `articles`, `services`, and `subscribers` data tables automatically:
```bash
php spark migrate
```

### 4. Serve the App Locally
Fire up the local execution sandbox loop to test responsive Bootstrap 5 templates:
```bash
php spark serve
```
The platform will go live immediately at: **`http://localhost:8080`**

---

## 🔒 Security Configuration Note
All routing segments mapped under the `admin` workspace rely on custom Auth filters (`app/Filters/AuthFilter.php`). Always verify token validation limits and rate-limit parsing layers on input forms to prevent bulk spamming vectors across communication channels.


## 📄 License & Ownership
Copyright © 2026 All Tropicals, LLC. All rights reserved. 

This repository and its entire codebase are **proprietary property**. Unauthorized copying, distribution, or modifications of these files via any medium is strictly prohibited.