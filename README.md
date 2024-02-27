# BlueSky-PDS Deployment Script

This script is designed to automate the initial deployment of BlueSky-PDS and its related components using Docker and bash scripting.
This is a free-to-use Bash script that allows you to easily install BlueSky-PDS and enhance its security with a single command. You can utilize this script on a blank server or an existing server, making it suitable for both new and experienced Bluesky-social/PDS server owners.
The script handles the entire BlueSky-PDS installation process, including activating the admin user. It ensures the security of your BlueSky-PDS server by changing the SSH port, installing a firewall, and automatically updating the firewall rules to reflect the new SSH port and installing Fail2Ban with progressive blocking rules.
The Bash file is unencrypted, freely usable, and redistributable (though credit to Honeytree Technologies is required).

## About the Script

- **Language**: Bash
- **Deployment**: Uses Docker images for deploying BlueSky-PDS containers.
- **Configuration**:
  - SSL certificate generation via Let's Encrypt for designated domains and Caddy setup.

## Pre-requisites
- Server or VPS with a minimum of 4GB Ram, 2 vCPU, and 65 GB storage.
- Ubuntu v22.04 LTS or 20.04 pre-installed.
- Open ports:  443, 80 and SSH (Which you will choose in the script).
- Machine should have internet access for fetching packages and Docker images.
- Pre-register the machine's IP with the domain for SSL certificate generation.

## Deployment Steps
1. SSH into the machine and assume root privileges.
2. Create and navigate to a directory: `mkdir auto_script && cd auto_script`.
    You can also use own directory.
3. Run the following command to start the script.
    ```bash
    curl -lO https://code.honeytreetech.com/fediverse/BlueSky-PDS/auto-installer/auto_script.sh && sudo chmod +x auto_script.sh && ./auto_script.sh
    ```
4. Input the requested details as per the following table.
    | Name | Description | Mandatory | Optional | Default Value | 
    |------|---------|-----------|----------|---------------|
    |`admin_email` | Admin email | &checkmark;|  &#10006;|  &#10006;| 
    |`domain_name` | Domain name| &checkmark;| &#10006;| &#10006;|
    |`port` | SSH port | &checkmark;| &#10006;| &#10006;|

5. Accept terms of service as prompted.
6. Create  PDS user account during installation of script.
7. Follow further on-screen instructions to complete the setup.
### Verifying that your PDS is online and accessible
You can check if your server is online and healthy by requesting the healthcheck endpoint.
You can visit `https://example.com/xrpc/_health` in your browser. You should see a JSON response with a version.
For example:
```
{"version":"0.2.2-beta.2"}
```
### Creating an account using pdsadmin
Using ssh on your server, use `pdsadmin` to create an account if you haven't already.
```bash
sudo pdsadmin account create
```
### Creating an account using an invite code
Using ssh on your server, use `pdsadmin` to create an invite code.
```bash
sudo pdsadmin create-invite-code
```
When creating an account using the app, enter this invite code.

### Using the Bluesky app with your PDS

You can use the Bluesky app to connect to your PDS.

1. Get the Bluesky app
    * [Bluesky for Web](https://bsky.app/)
    * [Bluesky for iPhone](https://apps.apple.com/us/app/bluesky-social/id6444370199)
    * [Bluesky for Android](https://play.google.com/store/apps/details?id=xyz.blueskyweb.app)
1. Enter the URL of your PDS (e.g. `https://example.com/`)

_Note: because the subdomain TLS certificate is created on-demand, it may take 10-30s for your handle to be accessible. If you aren't seeing your first post/profile, wait 30s and try to make another post._

### Updating your PDS

It is recommended that you keep your PDS up to date with new versions, otherwise things may break. You can use the `pdsadmin` tool to update your PDS.

```bash
sudo pdsadmin update
```
## Post Deployment
- Access BlueSky-PDS via the provided domain with the domain and invite code .
- SSH port defaults to new port (which you entered in the script).
- fail2ban is activated with progressive blocking.
## Post-Installation Security Recommendations

Once you have successfully deployed BlueSky-PDS using this script, it's crucial to take additional steps to secure and harden your environment. 
Consider the following actions:
- **Regular Updates**: Ensure that all system packages and software are regularly updated to patch potential vulnerabilities.
- **Firewall Configuration**: Fine-tune your firewall settings to allow only necessary traffic and block potential threats.
- **User Access**: Limit or disable root access. Use sudo for administrative tasks and avoid using the root account for daily tasks.
- **Secure Passwords**: Implement strong password policies, and consider using password managers.
- **Two-Factor Authentication**: Where possible, enable 2FA for critical services and accounts.
- **Backup**: Regularly back up critical data and ensure backups are stored securely.
- **Monitoring & Logging**: Set up monitoring and logging to detect and alert on suspicious activities.
- **Application-Specific Security**: Explore and implement security best practices specifically tailored to  BlueSky-PDS and any other applications you might be running.
- **Review and Audit**: Periodically review and audit your security settings and practices to ensure they are up-to-date with the latest threats and vulnerabilities.

It's essential to recognize that the security landscape is dynamic. Stay informed, and be proactive in securing your digital assets.
## CREDITS
This script and deployment guide have been made possible by [Honeytree Technologies, LLC](https://honeytreetech.com).

Please follow [@jeff@honeytree.social](https://honeytree.social/@jeff).