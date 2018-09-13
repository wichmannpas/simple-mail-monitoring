# Simple Mail Monitoring

This is a very simple script for email delivery checking/monitoring. It sends a test email with a random subject to the configured recipient address using the *local sendmail* configuration (e.g., SMTP on localhost).

Afterwards, it tries to retrieve that email using IMAP authenticating *on the remote mail server*. When it has successfully fetched the email, it writes the timestamp of that email into a file configured. This file can be read by another monitoring service to ensure that its value is recent enough. Especially, it is possible to serve that file from a web root to allow a remote monitoring server to retrieve it.

The script’s purpose is to be executed on a *different server* than the tested mailhost. This way, it can check whether external email delivery works as intended. Running it directly on the mailhost can cause some errors to go unnoticed, i.e., if only external email submission is affected.

## Using the script directly as a monitoring plugin (nagios, incinga etc.)

The purpose of this specific script is to provide an external monitoring server with the information about the last successful delivery. However, with slight modifications, it is possible to use it directly as a check command for nagios/icinga etc.
For that, it is required to remove the while-true in the main block at the bottom of the script. That will already provide a basic monitoring script which is able to check whether real-time email delivery is working (maybe requiring an increased check timeout).
