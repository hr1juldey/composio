## Why does a HighLevel Location installation fail or loop?

The `highlevel_location` toolkit connects to a sub-account. For company-level access, use [HighLevel Agency](/toolkits/highlevel_agency).

1. In your [Marketplace app's Auth settings](https://marketplace.gohighlevel.com/docs/Authorization/OAuth2.0/index.html), verify the client ID, client secret, **Target User**, and **Who can install**. Use a sub-account app and sign in as an administrator who can access the intended sub-account.
2. Request valid scopes for the endpoints you need. Use HighLevel's [scope reference](https://marketplace.gohighlevel.com/docs/Authorization/Scopes/). The Composio OAuth config defaults to `locations.readonly`; its `scopes` override is comma-separated. Add missing scopes in both HighLevel and Composio, then authorize again.
3. Match `oauth_redirect_uri` to the generated authorization URL and the Marketplace allowlist. The current toolkit default is `https://backend.composio.dev/api/v1/auth-apps/add`. Your application's final return URL is a separate redirect. Record the redirect chain to locate a loop.
4. Confirm that the installing administrator selected the intended sub-account. HighLevel [issues different token types](https://marketplace.gohighlevel.com/docs/Authorization/AccessTokenUseCase/index.html) depending on the install context and app distribution settings.

Create a fresh connection after correcting settings. If matching settings still fail, contact [support@composio.dev](mailto:support@composio.dev) with the auth config ID, connection ID, UTC timestamp, install context, and redacted redirect chain. Don't delete the auth config to retry an installation.

## How do I diagnose a HighLevel `versionId` or missing app version error?

Compare the generated authorization URL with your app's current Marketplace installation link. Record the app/version and both redacted URLs for support. `versionId` isn't an exposed auth-config field in the current Location schema, so don't invent an override or substitute an API version header.

Private apps support controlled testing; public distribution requires approval. Publishing publicly isn't a universal fix for an installation failure. If the current installation link also fails, escalate to HighLevel; if Composio generates a different failing URL, send that comparison to Composio support.

## Why is my HighLevel Location connection stuck in `INITIATED`?

`INITIATED` means the connection hasn't completed. Closing the browser can leave it there. Open a fresh connection link and complete account selection, consent, and the return to Composio.

If the callback completed but the account never becomes `ACTIVE`, contact support with the connection ID, UTC timestamp, selected sub-account, and redacted redirect chain or error. Repeatedly reinstalling can hide the original failure without fixing it. Use [generic connection troubleshooting](/docs/oauth-mcp-troubleshooting) for the evidence to include.
