```bash
$ npm install -g @hubspot/cli@latest

$ hs account auth

$ hs project create
```

Base contents -> App
Distribution -> marketplace
Auth type -> oauth
Features -> Webhooks

## Upload the Project to HubSpot

```sh
$ hs project upload
```

## Wire It Into Your Existing Node.js App **Connect HubSpot**

```sh
$ npm install @hubspot/api-client
```

```js
const hubspot = require("@hubspot/api-client");
const client = new hubspot.Client();

// Kick off OAuth
app.get("/oauth/hubspot", (req, res) => {
  const url = client.oauth.getAuthorizationUrl(
    process.env.HUBSPOT_CLIENT_ID,
    process.env.HUBSPOT_REDIRECT_URI,
    "crm.objects.contacts.read crm.objects.contacts.write crm.objects.deals.read crm.objects.deals.write crm.objects.owners.read",
  );
  res.redirect(url);
});

// Handle callback
app.get("/oauth/hubspot/callback", async (req, res) => {
  const tokens = await client.oauth.tokensApi.create(
    "authorization_code",
    req.query.code,
    process.env.HUBSPOT_REDIRECT_URI,
    process.env.HUBSPOT_CLIENT_ID,
    process.env.HUBSPOT_CLIENT_SECRET,
  );
  // Save tokens.access_token + tokens.refresh_token to your DB
  res.redirect("/dashboard?connected=true");
});
```

## Token Refresh (Critical!)

```js
async function getValidAccessToken(userId) {
  const tokens = await getTokensForUser(userId);

  // Refresh if expiring within 5 minutes
  if (Date.now() >= tokens.expiresAt - 5 * 60 * 1000) {
    const refreshed = await hubspotClient.oauth.tokensApi.create(
      "refresh_token",
      undefined,
      process.env.HUBSPOT_REDIRECT_URI,
      process.env.HUBSPOT_CLIENT_ID,
      process.env.HUBSPOT_CLIENT_SECRET,
      tokens.refreshToken,
    );

    await saveTokensForUser(userId, {
      accessToken: refreshed.access_token,
      refreshToken: refreshed.refresh_token,
      expiresAt: Date.now() + refreshed.expires_in * 1000,
    });

    return refreshed.access_token;
  }

  return tokens.accessToken;
}
```

## Use Tokens to Manage Leads

```js
// Fetch contacts (leads) for a user's connected HubSpot account
app.get("/leads", async (req, res) => {
  const accessToken = await getValidAccessToken(req.user.id);
  const client = new hubspot.Client({ accessToken });

  const contacts = await client.crm.contacts.basicApi.getPage(
    100, // limit
    undefined,
    ["firstname", "lastname", "email", "hs_lead_status"],
  );

  res.json(contacts.results);
});

// Create a new lead/contact
app.post("/leads", async (req, res) => {
  const accessToken = await getValidAccessToken(req.user.id);
  const client = new hubspot.Client({ accessToken });

  const contact = await client.crm.contacts.basicApi.create({
    properties: {
      firstname: req.body.firstName,
      lastname: req.body.lastName,
      email: req.body.email,
    },
  });

  res.json(contact);
});
```
