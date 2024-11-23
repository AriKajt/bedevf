# [Laravel Manual](https://laravel.com/docs/11.x)

# Laravel Essential Guide

## Setting Up a New Laravel Project

### Installation Requirements
- PHP >= 8.1
- Composer
- Node.js & NPM (for frontend assets)
- Database (MySQL, PostgreSQL, SQLite, or SQL Server)

### Creating New Project
```bash
# Via Composer
composer create-project laravel/laravel project-name

# Via Laravel Installer
composer global require laravel/installer
laravel new project-name
```

### Initial Configuration
1. Copy `.env.example` to `.env`
```bash
cp .env.example .env
```

2. Generate application key
```bash
php artisan key:generate
```

3. Configure database in `.env`:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

## Essential Artisan Commands

### Server
```bash
# Start development server
php artisan serve

# Clear various caches
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear
```

### Database & Migrations
```bash
# Create migration
php artisan make:migration create_users_table

# Run migrations
php artisan migrate

# Rollback migrations
php artisan migrate:rollback

# Reset and re-run all migrations
php artisan migrate:fresh

# Reset with seeders
php artisan migrate:fresh --seed
```

### Creating Components
```bash
# Create Model
php artisan make:model Post

# Create Model with migration
php artisan make:model Post -m

# Create Controller
php artisan make:controller PostController

# Create Resource Controller
php artisan make:controller PostController --resource

# Create Middleware
php artisan make:middleware CheckAge

# Create Seeder
php artisan make:seeder UserSeeder
```

## Common Migration Problems & Solutions

### 1. Table Already Exists
**Problem:**
```
[PDOException] SQLSTATE[42S01]: Base table or view already exists
```

**Solutions:**
```bash
# Drop all tables and migrate
php artisan migrate:fresh

# Check if table exists in migration
if (!Schema::hasTable('users')) {
    Schema::create('users', function (Blueprint $table) {
        // ...
    });
}
```

### 2. Foreign Key Constraints
**Problem:**
```
[PDOException] SQLSTATE[HY000]: General error: 1215 Cannot add foreign key constraint
```

**Solutions:**
- Ensure referenced table is created first (correct migration order)
- Check column types match exactly
- Use proper foreign key syntax:
```php
$table->foreignId('user_id')
      ->constrained()
      ->onDelete('cascade');
```

### 3. Column Already Exists
**Problem:**
```
[PDOException] SQLSTATE[42S21]: Column already exists
```

**Solutions:**
```php
// Check if column exists before adding
if (!Schema::hasColumn('users', 'email')) {
    $table->string('email');
}

// Or use table modification
Schema::table('users', function (Blueprint $table) {
    if (!Schema::hasColumn('users', 'email')) {
        $table->string('email')->after('name');
    }
});
```

### 4. Incorrect Data Type
**Problem:**
```
[PDOException] SQLSTATE[42000]: Syntax error or access violation
```

**Solution:**
- Double-check column types
- Common types:
```php
$table->id();
$table->string('name');
$table->text('description');
$table->integer('count');
$table->decimal('price', 8, 2);
$table->timestamp('published_at');
$table->timestamps();
```

## Best Practices

### Database
1. Always create migrations for database changes
2. Use meaningful names for migrations
3. Keep migrations small and focused
4. Always define foreign key relationships
5. Include indexes for frequently queried columns

### Models
1. Define relationships
2. Use proper attribute casting
3. Define fillable or guarded properties
4. Use model observers for complex operations

### Controllers
1. Follow RESTful conventions
2. Use resource controllers when appropriate
3. Keep controllers thin, move business logic to services
4. Use form requests for validation

### Routes
```php
// Basic routing
Route::get('/posts', [PostController::class, 'index']);

// Resource routing
Route::resource('posts', PostController::class);

// Route grouping
Route::middleware(['auth'])->group(function () {
    Route::resource('posts', PostController::class);
});
```

## Debugging Tips

1. Use Laravel's debug mode in `.env`:
```env
APP_DEBUG=true
```

2. Use Tinker for testing:
```bash
php artisan tinker
```

3. Use Laravel's error logging:
```php
Log::debug('Debug message');
Log::info('Info message');
Log::error('Error message');
```

4. Check Laravel log files in `storage/logs/laravel.log`

5. Use `dd()` or `dump()` for debugging:
```php
dd($variable);  // dump and die
dump($variable); // dump and continue
```
