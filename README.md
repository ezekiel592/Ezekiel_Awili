[README.md](https://github.com/user-attachments/files/34560345/README.md)
# WPU Login Setup

This project serves `Eawili_login.html` through an Express server and connects it to the MySQL database and table shown in phpMyAdmin: `ezzyvizzy.ezzy`.

## Configure MySQL

1. In phpMyAdmin, select the `ezzyvizzy` database and open the SQL tab.
2. Run the statements in `database-setup.sql`. This makes room for bcrypt password hashes and prevents duplicate usernames or emails. The table should have an auto-increment `id` column.
3. Copy `.env.example` to `.env`. Set `DB_USER` and `DB_PASSWORD` to the MySQL account used by phpMyAdmin. Set `SESSION_SECRET` to a new private random value; do not share or commit `.env`.

The MySQL account must be allowed to read and write `ezzy`, alter its indexes during setup, and create the session table used by the server.

## Run

From this project folder, run:

```powershell
npm install
npm start
```

Open `http://localhost:3000`. Do not open the HTML file directly; the form must be served by Express so `/api/login` and `/api/register` reach the backend.

The Create account option inserts a bcrypt-hashed password into `ezzy`. Login accepts either the username or email. Existing plain-text passwords are not accepted; reset them rather than storing or comparing passwords as plain text.

For deployment, use HTTPS and a private production MySQL account. For an actual university service, prefer the university's supported single sign-on if available.
