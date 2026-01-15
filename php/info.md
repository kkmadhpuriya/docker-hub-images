# Universal PHP 8.2 Apache Image

![Universal PHP Image](./docker-hub-banner.png)

## Short Description (for Docker Hub)

Production-ready PHP 8.2 Apache image optimized for Laravel, Symfony, and CodeIgniter. Includes essential extensions (PDO, MySQLi, GD, Zip) and enabled `mod_rewrite`. Features a configurable document root for flexible deployment of both modern and legacy applications. Multi-arch support (amd64/arm64).

---

This is a versatile, production-ready Docker image for PHP 8.2 applications running on Apache. It is pre-configured to support major PHP frameworks like **Laravel**, **Symfony**, and **CodeIgniter**, as well as custom PHP projects.

## 🚀 Key Features

- **Base Image**: Built on `php:8.2-apache`.
- **Extensions**: pre-installed with essential libraries:
  - `pdo`, `pdo_mysql`, `mysqli` (database support)
  - `gd` (image processing)
  - `zip` (archive management)
- **Web Server**:
  - Apache `mod_rewrite` enabled (essential for framework routing).
  - Configurable Document Root via Environment Variable.
- **Compatibility**: Designed for Laravel, Symfony, CodeIgniter, WordPress, and more.

---

## 🛠️ Usage Guide

### 1. Running a Laravel or Symfony Application

Modern frameworks like Laravel and Symfony usually serve files from a `public/` subdirectory. This image defaults to `/var/www/html/public` to support this out of the box.

Run the following command in your project root:

```bash
docker run -d \
  -p 80:80 \
  -v $(pwd):/var/www/html \
  --name my-laravel-app \
  kkmadhpuriya/php-laravel-codeigniter-symfony:8.2
```

- **`-v $(pwd):/var/www/html`**: Mounts your current directory (host) to the container's web root.
- **Result**: The server looks for `index.php` in `$(pwd)/public`.

### 2. Running CodeIgniter or Standard PHP

If your project's entry point is in the root directory (typical for CodeIgniter, older frameworks, or simple PHP scripts), you need to change the Document Root.

Override the `APACHE_DOCUMENT_ROOT` environment variable:

```bash
docker run -d \
  -p 80:80 \
  -v $(pwd):/var/www/html \
  -e APACHE_DOCUMENT_ROOT=/var/www/html \
  --name my-php-app \
  kkmadhpuriya/php-laravel-codeigniter-symfony:8.2
```

- **`-e APACHE_DOCUMENT_ROOT=/var/www/html`**: Tells Apache to serve files directly from the mounted root, not the `public` subdirectory.

### 3. Running with Custom Configuration

You can pass additional environment variables or mount custom configuration files if needed.

---

## 📦 Installed Extensions

- `mysqli`
- `pdo`
- `pdo_mysql`
- `gd` (with Freetype and JPEG support)
- `zip`

---

## 🏗️ Build & Publish (For Developers)

If you want to build and push your own version of this image:

### Build for Linux (amd64)

Essential if you are building on a Mac (M1/M2) for a production server.

```bash
docker build --platform linux/amd64 -t <user-name>/php-laravel-codeigniter-symfony:v1 .
```

### Push to Docker Hub

```bash
docker push <user-name>/php-laravel-codeigniter-symfony:v1
```
