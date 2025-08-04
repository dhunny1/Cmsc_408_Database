# cmsc-vcu/cmsc408-sp2025-semproj-template

Authors: Hunny Biguvu
# UTune Music app

UTunes is a personal music library management system designed to let users organize, play, and manage their favorite songs without ads, subscriptions, or hidden fees. It allows users to browse songs, create playlists, and favorite tracks, all through a clean web interface. UTunes is built for everyday listeners, students, DJs, and music collectors who want full control over their music collection.

This guide provides instructions on how to set up and run this project on your local machine.

## Prerequisites for UTunes music app

Before you begin, ensure you have the following installed:

* **Node.js and npm:** Download and install from [https://nodejs.org/](https://nodejs.org/)
* **SQLite3:** You need the command-line tool. Installation varies by OS (e.g., `sudo apt-get install sqlite3` on Debian/Ubuntu, `brew install sqlite3` on macOS).

## Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Install dependencies:**
    This project requires several Node.js packages. The core dependencies include: `express`, `sqlite3`, `cors`, `bcrypt` (or `bcryptjs`), `jsonwebtoken`, `nodemailer`, `passport`, `passport-google-oauth20`, `dotenv`, and `express-session`.

    *(Note: The original instructions listed multiple `npm install` commands with some overlapping or potentially redundant packages like `bcrypt` and `bcryptjs`. Ensure your `package.json` file correctly lists all necessary dependencies.)*

    Run the following command to install all dependencies listed in `package.json`:
    ```bash
    npm install
    ```
    *(If you don't have a `package.json`, you would need to install them manually, e.g., `npm install express sqlite3 cors bcryptjs jsonwebtoken nodemailer passport passport-google-oauth20 dotenv express-session`)*

## Configuration

1.  **Set up Environment Variables:**
    Create a file named `.env` in the root directory of the project. Add the following variables, replacing the placeholder values with your actual credentials:

    ```plaintext
    # .env file

    # Secret key for signing JWT tokens (choose a strong, unique secret)
    JWT_SECRET=your_super_secret_key

    # Gmail credentials for sending emails (e.g., password reset)
    # Use an "App Password" if you have 2FA enabled on your Google Account
    # See: [https://support.google.com/accounts/answer/185833](https://support.google.com/accounts/answer/185833)
    EMAIL_USER=your_gmail_account@gmail.com
    EMAIL_PASS=your_gmail_app_password

    # Google OAuth 2.0 Credentials for Google Sign-In
    GOOGLE_CLIENT_ID=YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com
    GOOGLE_CLIENT_SECRET=YOUR_GOOGLE_CLIENT_SECRET
    ```

2.  **Obtain Google OAuth Credentials:**
    * Go to the [Google Cloud Console](https://console.cloud.google.com/).
    * Create a new project or select an existing one.
    * Navigate to "APIs & Services" > "Credentials".
    * Click "Create Credentials" > "OAuth client ID".
    * Configure the consent screen if you haven't already.
    * Choose "Web application" as the application type.
    * Add Authorized JavaScript origins (e.g., `http://localhost:3000`).
    * Add Authorized redirect URIs (e.g., `http://localhost:3000/auth/google/callback`). Check your application's code for the exact callback URL required.
    * Click "Create". Copy the generated Client ID and Client Secret into your `.env` file.
    * *(Note: The original instructions mentioned enabling the Google+ API, which is deprecated. You typically need the "Google People API" or similar identity-related APIs depending on the scopes requested by Passport.)* Further instructions can be found here: [Google Sign-In for Websites](https://developers.google.com/identity/sign-in/web/sign-in)

3.  **Create and Populate the Database:**
    Make sure you have a `database.sql` file containing the necessary SQL commands to create your tables. Run the following command in your terminal from the project's root directory:
    ```bash
    sqlite3 database.db < database.sql
    ```
    This will create a `database.db` file (or whatever name you choose) and execute the SQL script to set up the schema.

4.  **Add Media Files:**
    * Place your music files (e.g., `.mp3`) into the `/songs/` directory.
    * Place the corresponding album art images into the `/images/` directory.

## Running the Application

1.  **Start the server:**
    ```bash
    node server.js
    ```

2.  **Access the application:**
    Open your web browser and navigate to:
    [http://localhost:3000](http://localhost:3000)
    

---

