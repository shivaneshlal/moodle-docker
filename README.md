# moodle-docker

Run [Moodle](https://moodle.org/) locally using Docker with **Nginx**, **PHP-FPM**, and **PostgreSQL**.

---

## Quick Start

**Clone this repo**
  ```bash
   git clone git@github.com:shivaneshlal/moodle-docker.git
   cd moodle-docker
   git clone --branch MOODLE_500_STABLE https://github.com/moodle/moodle.git moodle

   # Set the creds in the .env
   DB_NAME=moodle
   DB_USER=moodle
   DB_PASSWORD=changeme

docker compose up -d --build

