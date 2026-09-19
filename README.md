# osTicket Help Desk Lab (Docker Compose on Windows)

A local help desk ticketing system built with Docker Compose. It runs osTicket and a MySQL database in two containers on Windows, and I used it to practice the ticket lifecycle: submitting tickets as a user, then triaging, assigning, replying to and closing them as staff.

This is a learning lab, not a production deployment. The users, emails and tickets are fictional.

## What this project shows

- Deploying a two-container application with Docker Compose (osTicket and MySQL 5.7)
- Passing configuration through a `.env` file and connecting containers by service name
- Keeping database data with a named volume
- Troubleshooting a real Docker Desktop failure on Windows (see [Troubleshooting](#troubleshooting))
- Working tickets in the osTicket admin panel: priorities, assignment to a second staff account, replies and closure

## Architecture

```
Browser (localhost:8080)
        |
        v
+--------------------+      Docker network      +-----------------+
| osTicket container |  <-------------------->  | MySQL container |
| (web app, port 80) |     MYSQL_HOST=mysql     | (mysql:5.7)     |
+--------------------+                          +--------+--------+
                                                         |
                                                named volume: mysql_data
```

- Port 8080 on the host maps to port 80 in the osTicket container.
- osTicket finds the database by the service name `mysql`.
- The `mysql_data` volume keeps tickets and users when the containers are stopped.

## Tech used

Docker Desktop, Docker Compose, WSL 2, MySQL 5.7, osTicket, Windows Command Prompt

## Run it (Windows CMD)

1. Install Docker Desktop for Windows with the WSL 2 backend, and wait for the engine to show as running.
2. Clone this repo and open the folder in CMD.
3. Create your own `.env` from the example and set your own passwords:
   ```
   copy .env.example .env
   notepad .env
   ```
4. Start the lab:
   ```
   docker compose up -d
   docker ps
   ```
   The first run downloads the images. osTicket shows `(healthy)` after about a minute.
5. Open the portals:
   - User portal: `http://localhost:8080`
   - Staff panel: `http://localhost:8080/scp/login.php`
6. Stop it:
   ```
   docker compose down
   ```
   Use `docker compose down --volumes` to also delete all data.

The staff login is the default account from the original lab guide. Don't reuse it, and don't expose port 8080 to the internet.

## Screenshots

**Starting the lab with Docker Compose**
![Docker Compose up](screenshots/01-compose-up.png)

**Both containers running, osTicket healthy**
![docker ps](screenshots/02-docker-ps.png)

**User portal: opening a ticket**
![Open a new ticket form](screenshots/03-open-ticket-form.png)

**Confirmation shown to the user**
![Ticket created](screenshots/04-ticket-created.png)

**Staff queue when the tickets arrive**
![Queue at intake](screenshots/05-queue-intake.png)

**Triage: tickets assigned to a second staff account**
![Queue after assignment](screenshots/06-queue-assigned.png)

**A staff reply to a user**
![Staff reply](screenshots/07-staff-reply.png)

**Closed tickets**
![Closed queue](screenshots/08-closed-queue.png)

## Ticket scenarios

I wrote realistic test tickets to work through, such as an account lockout, a phishing report, a software request, a new-hire setup and a laptop that won't boot. Six test tickets were submitted. I assigned two to a second staff account and resolved two with staff replies. The rest were left open on purpose, for example while waiting on approval. The scenarios, sample replies and internal notes are in [tickets.md](tickets.md).

## Troubleshooting

**Problem:** `docker compose up -d` failed with `request returned 500 Internal Server Error ... dockerDesktopLinuxEngine`.

**What I checked:**
- `docker compose config` printed the parsed file correctly, so the project files were fine.
- `docker version` showed the Client section but no Server section, so the Docker engine wasn't responding.
- `wsl --list --verbose` printed a help screen instead of a list, and `wsl --status` printed nothing. That showed WSL wasn't installed.

**Cause:** Docker Desktop on Windows needs WSL 2, and it wasn't installed.

**Fix:**
```
wsl --install --no-distribution --web-download
```
I restarted the PC, confirmed `wsl --status` showed version 2, opened Docker Desktop, and then `docker version` showed the Server section and `docker compose up -d` worked.

## What I learned

- How an application and its database run as separate containers and find each other by service name
- How to diagnose a failing service by checking one layer at a time (project file, Docker client, engine, WSL)
- How a help desk workflow fits together: intake, priority, assignment, internal notes, replies and closure

## Credits and notes

- osTicket is an open-source ticketing system. This lab is based on a beginner osTicket and Docker video lab guide, which I adapted for Windows Command Prompt.
- The `devinsolutions/osticket` image is used instead of the official image, following that guide, which noted a PHP parsing error with the official one.
- `.env` holds local settings and is not committed. Copy `.env.example` and set your own values.
