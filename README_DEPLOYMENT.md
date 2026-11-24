# CivicTrack — deployment package

This package contains the application's Python source, pages, modules, database schema/migration scripts, and Streamlit configuration.

## Run locally

1. Install Python 3.10 or newer.
2. Create and activate a virtual environment.
3. Install dependencies: `pip install -r requirements.txt`
4. Start the app: `streamlit run streamlit_app.py`

The application creates missing SQLite tables on first launch using the existing `CREATE TABLE IF NOT EXISTS` initializer.

## Deploy to Streamlit Community Cloud

1. Create a GitHub repository and upload the contents of this folder.
2. In Streamlit Community Cloud, create an app from that repository.
3. Set the main file path to `streamlit_app.py`.
4. Add any required secrets in the Streamlit app's Secrets settings, not in GitHub.

For email password-reset delivery, configure:

```toml
GMAIL_APP_PASSWORD = "your-new-gmail-app-password"
```

The sender address is currently configured in `modules/email_service.py`. Only configure a Gmail app password for the account that is authorized to send from that address, or update the sender address in the code to an account you control.

## Important data and privacy notes

- The original `secrets.toml`, SQLite databases/backups, and uploaded complaint photographs/videos were intentionally excluded. They may contain credentials or personal information.
- Existing local accounts and complaint records are **not** included. The deployment starts with a fresh database. Create/seed an administrator account using the project's approved setup process after checking the administrator identity and configuration.
- The current application stores records in a local SQLite database and media in a local `uploads/` directory. Streamlit Community Cloud's local filesystem is not a durable production database/file store. Use managed persistent database and object storage before accepting real public complaints.
- Do not run `database/upgrade_security.py` on a live database without reviewing it: its source includes account-deletion behavior.
- Review the migration scripts before running any of them against important data.
- Do not commit passwords, API keys, real complaint records, or citizen uploads to GitHub.
- Rotate any credentials that were present in the original archive before deploying.

This is a deployment-preparation package, not a security audit or guarantee that every workflow is production-ready.
