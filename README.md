# merit/press Certificate Studio — Hostinger Deployment

Production-ready Hostinger Node.js bundle for merit/press Certificate Studio.

This repository contains the compiled application only. It is designed to be connected to a Hostinger Node.js application.

## GitHub repository details

### Suggested repository name

```text
merit-press-hostinger
```

### Suggested description

```text
Production-ready Hostinger Node.js deployment bundle for merit/press Certificate Studio.
```

### Suggested GitHub topics

```text
hostinger
nodejs
certificate-generator
certificate-maker
academy-tools
education
pdf-generation
email-automation
smtp
nodemailer
```

## Repository contents

The repository must have this structure at its root:

```text
.
├── package.json
├── public/
│   ├── index.html
│   └── ...
└── dist/
    ├── index.mjs
    └── ...
```

Do not place these files inside another `hostinger-upload/` folder in the GitHub repository. `package.json`, `public/`, and `dist/` must be at the repository root.

## Deploy from GitHub to Hostinger

### 1. Create the GitHub repository

Create a new GitHub repository named:

```text
merit-press-hostinger
```

Upload the **contents** of the `hostinger-upload` folder to the root of that repository.

### 2. Create a Node.js application in Hostinger

In Hostinger hPanel:

1. Open the website where you want to run the app.
2. Open **Node.js Apps**.
3. Create a new Node.js application.
4. Connect your GitHub account.
5. Select the `merit-press-hostinger` repository.
6. Select the deployment branch, normally `main`.
7. Set the application root to the cloned repository root.

The exact menu names can vary by Hostinger plan.

### 3. Configure the Node.js application

Use these settings:

```text
Application mode: Production
Startup file: dist/index.mjs
Environment variable: NODE_ENV=production
```

Choose a Node.js version supported by your Hostinger plan.

Hostinger should provide the application `PORT` automatically. Do not hardcode a port.

### 4. Install dependencies

Inside the application root, run:

```bash
npm install
```

### 5. Start the application

Run:

```bash
npm start
```

Or use Hostinger’s **Start**, **Deploy**, or **Restart application** button.

The start command is already defined in `package.json`:

```bash
node --enable-source-maps dist/index.mjs
```

## Connect your domain

Attach the Node.js application to your Hostinger domain or subdomain, then open:

```text
https://your-domain.com
```

Enable SSL/HTTPS in Hostinger if it is not enabled automatically.

## Application pages

Public pages:

```text
/
/about
/contact
/privacy
/terms
```

Workspace pages:

```text
/workspace
/design
/recipients
/settings
/automate
```

## Test the live application

1. Open the website domain.
2. Open `/automate`.
3. Click **Add your own template**.
4. Upload a blank certificate artwork image.
5. Confirm the artwork preview appears.
6. Drag **Morgan Bell** onto the blank name line.
7. Release the name and confirm its position is saved.
8. Open **Email setup**.
9. Enter a verified SMTP configuration.
10. Upload a one-person CSV roster.
11. Launch the batch.
12. Confirm the received PDF contains the original artwork and the student name in the selected position.

Example test CSV:

```csv
Name,Email
Test Student,your-email@example.com
```

Use an email inbox you control for the first test.

## Updating the application

This is a generated deployment bundle. It is not the development source repository.

When the application changes:

1. Open the original source project.
2. Run:

   ```bash
   pnpm run hostinger:build
   ```

3. Replace the contents of this GitHub repository with the newly generated `hostinger-upload` contents.
4. Commit and push the changes.
5. Allow Hostinger to redeploy from GitHub, or click **Deploy/Restart** in Hostinger.

After an update, the repository root must still contain:

```text
package.json
public/
dist/
```

## SMTP configuration

Each academy enters its own SMTP settings inside the application’s **Email setup** page.

Required values include:

- SMTP host
- SMTP port
- Sender email
- SMTP password
- Sender name
- Email subject and body
- Optional reply-to address

Do not commit SMTP passwords or other credentials to GitHub.

## Temporary session behavior

This application intentionally does not use a database.

The following are kept temporarily in server memory:

- Uploaded certificate templates
- Uploaded artwork
- Recipient lists
- SMTP settings
- Batch history

This information is cleared when the Node.js process restarts and expires after inactivity. Restarting or redeploying the Hostinger application will require academies to upload or enter their temporary session information again.

## Why Hostinger Node.js is required

This bundle includes both:

- The compiled React website in `public/`
- The Express API and PDF/email server in `dist/`

It must run as a Node.js application. Do not deploy this bundle as a static-only website.

## License

This project is licensed under the MIT License.