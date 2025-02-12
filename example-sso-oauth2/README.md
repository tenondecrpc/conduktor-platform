# Run Conduktor Platform locally with auth0

This example run conduktor-platform using an Oauth2 SSO configuration providing users for login.

<!-- TOC -->
* [Run Conduktor Platform locally with auth0](#run-conduktor-platform-locally-with-auth0)
  * [Requirements](#requirements)
  * [Configuration](#configuration)
    * [Auth0](#auth0)
    * [Okta](#okta)
    * [Keycloak](#keycloak)
<!-- TOC -->


## Configuration

### Auth0
Configure a new Application on Auth0 :

- **Step 1**: create regular web application
![](assets/auth0-app-step1.png)

- **Step 2**: get client Id/Secret and domain
![](assets/auth0-app-step2.png)

- **Step 3**: configure callback url
![](assets/auth0-app-step3.png)

> Note: Conduktor platform expose a callback URI for Oauth2 authentication flow. 
>This URL is defined as `http://<platform hostname>/oauth/callback/<oauth2 config name>`.

- **Step 4**: save changes
![](assets/auth0-app-step4.png)

Platform configuration : 
Add the following yaml fragment to your input `platform-config.yml` file. See [here](../doc/Configuration.md) for platform configuration.
```yaml
sso:
  oauth2:
    - name: "auth0"
      default: true
      client-id: "<auth0 app client id>"          # Get from step2 - 2
      client-secret: "<auth0 app client secret>"  # Get from step2 - 3
      openid:
        issuer: "<auth0 app domain>.auth0.com"    # Get from step2 - 1 
```

### Okta
Configure a new Application on Okta :

- **Step 1**: create OpenId Connect web application
![](assets/okta-app-step1.png)

- **Step 2**: configure callback url
![](assets/okta-app-step2.png)

> Note: Conduktor platform expose a callback URI for Oauth2 authentication flow. 
>This URL is defined as `http://<platform hostname>/oauth/callback/<oauth2 config name>`.

- **Step 3**: configure app assignment and save changes
![](assets/okta-app-step3.png)

- **Step 4**: Get client Id/Secret
![](assets/okta-app-step4.png)

Platform configuration :
Add the following yaml fragment to your input `platform-config.yml` file. See [here](../doc/Configuration.md) for platform configuration.
```yaml
sso:
  oauth2:
    - name: "okta"
      default: true
      client-id: "<okta app client id>"          # Get from step4 - 8
      client-secret: "<okta app client secret>"  # Get from step4 - 9
      openid:
        issuer: "<okta domain>.okta.com"         # Your okta domain
```

### Keycloak
Configure a new client on Keycloak :

- **Step 1**: create new OpenId Connect client
![](assets/keycloak-app-step1.png)


- **Step 2**: Select Client auth flows 
![](assets/keycloak-app-step2.png)


- **Step 3**: Configure redirect url 
![](assets/keycloak-app-step3.png)

> Note: Conduktor platform expose a callback URI for Oauth2 authentication flow. 
>This URL is defined as `http://<platform hostname>/oauth/callback/<oauth2 config name>`.

- **Step 4**: Get client secret
![](assets/keycloak-app-step4.png)


Platform configuration : 
Add the following yaml fragment to your input `platform-config.yml` file. See [here](../doc/Configuration.md) for platform configuration.
```yaml
sso:
  oauth2:
    - name: "keycloak"
      default: true
      client-id: "<keycloak client id>"                    # Created step 1 - 2
      client-secret: "<keycloak client id>"                # Get from step 4 - 5
      openid:
        issuer: "http://<host(:port)>/realms/<realm name>" # Could be get from the OpenI Endpoint configuration (.well-known) output on Realm settings page.
```
