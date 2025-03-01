# Jira Webhook (*proof of concept*)

Grant temporary access to SDM resources via Jira using webhooks.

## How it works

The user interested in getting access to a resource, needs to create an issue with the description: `access to resource-name`. The webhook grants access if the issue is assigned to a valid SDM_ADMIN and closed.

## Configure

1. Generate API Token [here](https://id.atlassian.com/manage-profile/security/api-tokens)
2. Enable organization visibility for users emails [here](https://id.atlassian.com/manage-profile/profile-and-visibility) - you need to do this for all users, due to [GDPR](https://community.developer.atlassian.com/t/guidelines-for-requesting-access-to-email-address/27603).
3. Configure webhook: https://`<domain-id>`.atlassian.net/plugins/servlet/webhooks
    - The script uses [ngrok](https://ngrok.com/) for creating a valid HTTPS endpoint. If you need to deploy in prod you'll need proper certs - cannot use self-signed.
    - If you use ngrok, copy the Tunnel URL you get when running the server. For example: `https://ac3b-80-31-185-170.ngrok.io/weebhook`. IMPORTANT: Use HTTPS

## Run

You need to define the following variables:
```
JIRA_USER=<jira-user> # Usually an email address
JIRA_TOKEN=<jira-token>
JIRA_BASE_URL=https://<domain-id>.atlassian.net
SDM_API_ACCESS_KEY=<sdm-api-access-key>
SDM_API_SECRET_KEY=<sdm-api-secret-key>
SDM_ADMINS=<sdm-admins> # A list of email addresses separated by spaces
```

After installing all the dependencies listed in [requirements.txt](requirements.txt), start the server:
```
python3 server.py
```
