# office capacity

When you are using Officient [https://www.officient.io/] you might be using the feature to enter 'work from home' days. 
This project gathers this data from the officient calendar and groups the data to calculate the total capacity in the office. During COVID it is important to have a clear view on the maximum capacity. 

By using n8n to connect to the officient API we were able to build this visualisation in a very short time. We want to help other officient users with this configuration to quickly get a good overview.

## Installation

This repo contain two parts:
- n8n configuration
- quick web tool to visualise office capacity

### N8N configuration

1. **N8N installation:**
    make sure you have n8n running on your server. You can find all installation options on the n8n website: https://docs.n8n.io/getting-started/installation/
    If you have docker running, this command spins up an instance:
    ```docker run --restart unless-stopped -it \
            --name n8n \
            -p 5678:5678 \
            -v ~/.n8n:/home/node/.n8n \
            n8nio/n8n \
            n8n start --tunnel
    ```
    The `--tunnel` option is important is you don't want to expose your n8n installation to the internet. 
2. **N8N:** Open the n8n instance and import the n8n configuration from this repository.
2. **Officient:** Create a new app in the `Officient` developers portal: https://aaltra.officient.io/developer 
    the minimum access rights for this configuration are: `basics` and `calendar`. 
3. **N8N:** Add your officient credentials to the instance. Click on the `credentials` icon on the left and choose `new`.
   Choose `OAuth2 API` from the list of credentials.
   Fill out the following values:
   - Authorization URL: `https://app.officient.io/authorize`
   - Access token URL: `https://api.officient.io/1.0/token`
   - Client ID: `from your officient app`
   - Client secret: `from your officient app`

4. **N8N:** Copy the OAuth redirect URL from the credentials
5. **Officient:** Edit the officient app and paste the redirect URL in the field `Redirect URI`
6. **N8N:** select the newly created credentials on one of the officient nodes
7. **N8N:** save the configuration and mark it as `active`
8. **N8N:** go to the first webhook node and copy the production URL

You can test your configuration by pasting the copied URL in your webbrowser. 
You can use this URL in any data visualisation program to visualise the capacity in your office.

### web tool visualisation

1. Edit the index.html and paste the copied URL from N8N in the variable `n8nWebhookUrl`
2. If you want to test, you can run `node testLocally.js` in the webserver folder
3. open http://localhost:8080 to see your visualisation run! 
4. For production purposes, copy the edited index.html to your own webserver.
   