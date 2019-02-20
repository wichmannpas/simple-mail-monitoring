# Simple Mail Monitoring

This is a very simple script for email delivery checking/monitoring. It sends a test email with a random subject to the configured recipient address using a configured SMTP configuration (e.g., SMTP on localhost).

Afterwards, it tries to retrieve that email using IMAP authenticating *on the remote mail server*. When it has successfully fetched the email.
It writes a scrape result in the prometheus textfile format.
This can be read by prometheus to collect metrics and allow alerts using alertmanager.

The script’s purpose is to be executed on a *different server* than the tested mailhost.
This way, it can check whether external email delivery works as intended.
Running it directly on the mailhost can cause some errors to go unnoticed, i.e., if only external email submission is affected.

To deploy this script, adapt the `config.py.example` as `config.py` and register a cron to periodically call this script depending on your requirements, e.g., every 15 minutes.
