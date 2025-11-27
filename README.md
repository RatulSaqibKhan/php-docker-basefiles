# PHP Docker Basefiles

A collection of <b>base Dockerfiles</b>, <b>config files</b>, and <b>environment setups</b> for building consistent, production-ready PHP application images.<br>
This repository organizes reusable templates for PHP environments such as <b>Apache, CLI, FPM, Alpine</b>, and more — allowing you to standardize Docker images across multiple PHP projects.

## 🚀 Purpose

- The goal of this repository is to:
- Provide <b>foundation Dockerfiles</b> for various PHP versions and runtimes.
- Maintain unified, reusable <b>base configurations</b> (extensions, tools, scripts).
- Reduce duplicate setup across multiple PHP applications.
- Enable quick creation of application-specific Docker images on top of these bases.

## 📁 Repository Structure

```bash
php-docker-basefiles/
│
├── README.md
│
├── php8.4-apache/
│   ├── Dockerfile
│   └── entrypoint.sh
│
└── shared/
    ├── scripts/
    ├── configs/
    └── README.md
```
## 🧱 Available Base Images

This repository may include different types of base images:

- PHP + Apache
- PHP CLI
- PHP-FPM
- Debian-based or Alpine-based
- Variant builds with additional extensions
  - Redis
  - Cassandra
  - GD
  - Intl
  - Opcache
  - Composer
  - Supervisor (optional)

## 🛠️ Usage
1. Clone the repo
    ```bash
      git clone https://github.com/RatulSaqibKhan/php-docker-basefiles.git
    ```
2. Choose a base image directory <br>
    For example, using php8.4-apache:
    
    ```bash
      cd php8.4-apache
    ```

3. Build the Docker image
    ```bash
      docker build -t base-php84-apache .
    ```

4. Extend in your application <br>
    In your app's Dockerfile:
    ```bash
      FROM base-php84-apache

      COPY ./codes /var/www/html
    ```
## 📦 Included Features

Depending on each variant, the images may include:

- Composer (latest)
- Common PHP extensions (pdo, mbstring, intl, gd, zip, opcache)
- Custom Apache vhost configs
- Entrypoint scripts
- System dependencies for frameworks like Laravel, Symfony, or custom apps

## 🔧 Customization

Inside each variant folder, you can:

- Add more PHP extensions
- Add custom .ini files
- Modify Apache or FPM configs
- Extend the base to match project-specific needs
- Each base image is intentionally minimal, so you can build on top of it as required.

## 📝 Contributing

Feel free to:

- Add new PHP versions
- Add support for FPM, Alpine, or Nginx-based images
- Improve scripts and configuration
- Submit issues or pull requests

## 📄 License

This repository is released under the [MIT License](./LICENSE).