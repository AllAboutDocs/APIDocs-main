# authentication and authorization

Every API request requires an authenticated session. The Docs Gateway service provides an independent interface through which third parties can use Docs services, by implementing authentication through Docs STS (Docs Security Token Service). STS is an OAuth2 server designed to provide the means of authentication, authorization, and accounting for service-to-service communication. STS provides each service with an identity that enables other services to trust it.

* **Authentication** - Authentication is the act of proving an assertion, to verify the user or the service identity.
* **Authorization** - Authorization is the process of specifying access rights to a user or a service.
* **Scopes** - Scopes provide a way to limit the amount of access that's granted to an access token.

STS ensures that the proper authentication and security measures are in place before interacting with the services that the Docs teams own. Docs STS service provides authentication/authorization/token management and only the scope is managed by the Global Docs service.

## Generate token for Docs Gateway STS integration

To generate an STS token, perform the following steps:

{% stepper %}
{% step %}
### Download the production script

Download `generate_token_prod.sh` for production.
{% endstep %}

{% step %}
### Save the script locally

Save the script locally to the `generate_token.sh` file.
{% endstep %}

{% step %}
### Make the script executable

Run `chmod +x ./generate_token_prod.sh`
{% endstep %}

{% step %}
### Add the private key

Copy the `Docs Gateway - STS Client` secret key for the related environment from 1Password and store it in the `sts_private_key.pem` file in the same directory where you stored the script.
{% endstep %}

{% step %}
### Generate the token

Run this command to generate the token:

`./generate_token.sh ${ClientId} ${KeyId} sts_private_key.pem (Ex. ./generate_token.sh ft-Docs-gateway-tester 9602ac55-46f0-4296-aea6-a5bfdbd845b9 sts_private_key.pem)`
{% endstep %}

{% step %}
### Add the authentication header

Add the Authentication header and use the token as value.
{% endstep %}

{% step %}
### Create a Docs using Docs Gateway

Create a Docs using Docs Gateway (with Docs STS), Docs Workflow and the Docs Service. Replace `ACCESS_TOKEN_GOES_HERE`.

```json
curl -X POST --location "http://localhost:8084/v1/docs" \
 -H "Accept: application/json" \
 -H "Content-Type: application/json" \
 -H "Authorization: Bearer ACCESS_TOKEN_GOES_HERE" \
 -d "{
\"countryCode\": \"PK\",
\"description\": \"My first Docs\",
\"externalReferenceId\": \"Docs-test\",
\"subsidiaryId\": 2
}"
```
{% endstep %}
{% endstepper %}
