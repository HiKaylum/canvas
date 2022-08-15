# Canvas

Just playing around with Svelte

## Setup

You will need to create an [Auth0](https://auth0.com/) account and create a [tenant](https://auth0.com/docs/get-started/auth0-overview/create-tenants). Once one is created click `Create Application`

![Create Application](https://i.gyazo.com/41ba81c7ebca34107396e8c421d38a91.png)

A popup will appear, name your app and select `Single Page Web Applications`. 

![Create Application Popup](https://i.gyazo.com/631ba5dd6571c5fdd898033d232f66e7.png)
  
Once this is done click on `settings` and add `http://localhost:5173/` to the following;

1. Allowed Callback URLs
2. Allowed Logout URLs
3. Allowed Web Origins

Then create a file in the root directory `.env.development` and add the following entries:

```
VITE_AUTH0_DOMAIN=AUTH0_DOMAIN_HERE
VITE_AUTH0_CLIENT_ID=AUTH0_CLIENT_ID_HERE
```

Once done you to start the dev server run:

```bash
# Install packages
npm i

# Run dev server
npm run dev -- --open
```
