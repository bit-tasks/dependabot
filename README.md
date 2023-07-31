# Dependabot
This repository shows how to use Dependabot to install newer versions of Bit Component dependencies.

- [Dependabot Config](https://github.com/bitdev-community/dependabot-demo/blob/main/.github/dependabot.yml)
- [Dependabot Results](https://github.com/bitdev-community/dependabot-demo/network/updates)

Below are the steps to set up Dependabot for your Bit project.

**Note:** Your project should include a `package.json` for dependabot to work.

## Step 1: Set Up Dependabot Secret

1. Go to the "Settings" section in your repository.
2. Create a secret named `BIT_CONFIG_USER_TOKEN` under "Secrets and variables" -> "Dependabot" and for the value use [Bit token](https://bit.dev/reference/config/bit-config/#user.token) with the right permission level.

## Step 2: Configure Dependabot for Bit

Create a file named `dependabot.yml` under the .github directory and add the following configuration:
```
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"
    groups:
      showoff-scope-dependencies:
         patterns:
           - "@showoff*"
```

Note: The above configuration instructs Dependabot to check for new version updates only in the Bit scope `@showoff`.

## Step 3: Create a `.npmrc` File with NPM Registries, including Bit Registry

1. At the root level of your project (next to `package.json`), create a file named `.npmrc`.
2. Add the following registries to the `.npmrc` file:

At your project root level (next to package.json), create a file named `.npmrc` and add the following registries.

```
registry=https://registry.npmjs.org/
@showoff:registry=https://node-registry.bit.cloud
@bit:registry=https://node.bit.cloud
@teambit:registry=https://node-registry.bit.cloud
//node.bit.cloud/:_authToken=${BIT_CONFIG_USER_TOKEN}
```

**Note:** The above configuration includes packages from `@showoff` [Bit org](https://bit.cloud/showoff).

By following these steps and configurations, you'll have Dependabot set up to automatically handle your project's newer versions of Bit Component dependencies.
