# [Backstage](https://backstage.io)

This is your newly scaffolded Backstage App, Good Luck!

To start the app, run:

```sh
yarn install
yarn start
```

## Issues

- [solved] catalog failed to sync user from keycloak
  ```shell
    2026-09-02T17:49:14.614Z search warn Index for techdocs was not created: indexer
    received 0 documents documentType="techdocs"2026-09-02T17:49:14.614Z search info
    Collating documents for techdocs succeeded
    documentType="techdocs"2026-09-02T17:49:14.620Z rootHttpRouter info
    [2026-09-02T17:49:14.620Z] "GET /api/catalog/entities/by-query?limit=500
    HTTP/1.1" 200 0 "-" "node-fetch/1.0 (+https://github.com/bitinn/node-fetch)"
    type="incomingRequest" date="2026-09-02T17:49:14.620Z" method="GET"
    url="/api/catalog/entities/by-query?limit=500" status=200 httpVersion="1.1"
    userAgent="node-fetch/1.0
    (+https://github.com/bitinn/node-fetch)"2026-09-02T17:49:14.624Z search info
    Collating documents for software-catalog succeeded
    documentType="software-catalog"2026-09-02T17:49:16.583Z catalog error Failed to
    authenticate class="KeycloakOrgEntityProvider"
    taskId="KeycloakOrgEntityProvider:default:refresh"
    taskInstanceId="6707446b-c6db-4573-a3de-1ccb997adc65"2026-09-02T17:49:16.588Z
    catalog error Error while syncing Keycloak users and groups Cannot read
    properties of undefined (reading 'split') class="KeycloakOrgEntityProvider"
    taskId="KeycloakOrgEntityProvider:default:refresh"
    taskInstanceId="6707446b-c6db-4573-a3de-1ccb997adc65" name="TypeError"
    cause=undefined stack="TypeError: Cannot read properties of undefined (reading
    'split')\n at decodeToken
    (/Users/essan/Code/backstage/node_modules/@keycloak/keycloak-admin-client/src/utils/decode.ts:6:29)\n
    at KeycloakAdminClient.setRefreshToken
    (/Users/essan/Code/backstage/node_modules/@keycloak/keycloak-admin-client/src/client.ts:147:33)\n
    at KeycloakAdminClient.auth
    (/Users/essan/Code/backstage/node_modules/@keycloak/keycloak-admin-client/src/client.ts:116:10)\n
    at process.processTicksAndRejections (node:internal/process/task_queues:104:5)\n
    at async Object.authenticate
    (/Users/essan/Code/backstage/node_modules/@backstage-community/plugin-catalog-backend-module-keycloak/src/lib/authenticate.ts:78:5)\n
    at async KeycloakOrgEntityProvider.read
    (/Users/essan/Code/backstage/node_modules/@backstage-community/plugin-catalog-backend-module-keycloak/src/providers/KeycloakOrgEntityProvider.ts:232:5)\n
    at async Object.fn
    (/Users/essan/Code/backstage/node_modules/@backstage-community/plugin-catalog-backend-module-keycloak/src/providers/KeycloakOrgEntityProvider.ts:290:13)\n
    at async
    <anonymous>
    (/Users/essan/Code/backstage/node_modules/@backstage/backend-defaults/src/entrypoints/scheduler/lib/PluginTaskSchedulerImpl.ts:250:13)\n
    at async TaskWorker.fn
    (/Users/essan/Code/backstage/node_modules/@backstage/backend-defaults/src/entrypoints/scheduler/lib/PluginTaskSchedulerImpl.ts:247:9)\n
    at async TaskWorker.runOnce
    (/Users/essan/Code/backstage/node_modules/@backstage/backend-defaults/src/entrypoints/scheduler/lib/TaskWorker.ts:284:7)\n
    at async
    <anonymous>
        (/Users/essan/Code/backstage/node_modules/@backstage/backend-defaults/src/entrypoints/scheduler/lib/TaskWorker.ts:96:31)"
        status=undefined</anonymous
    ></anonymous
    >
  ```
  **solution**
  ```
  Grant Refresh Tokens to Service Accounts in KeycloakYou can force Keycloak to include a refresh_token when Backstage authenticates by configuring the OpenID Connect client properties.
  1. Log in to your Keycloak Admin Console.
  2. Navigate to Clients and select your backstage-catalog client.
  3. Scroll down or go to the Advanced settings tab.
  4. Locate the OpenID Connect Compatibility Modes or Advanced Settings block.
  5. Toggle Use Refresh Tokens For Client Credentials (or "Use Refresh Tokens") to On.
  6. Save the settings and restart your Backstage application.
  ```
