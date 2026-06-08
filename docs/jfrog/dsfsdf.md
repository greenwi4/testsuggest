---
title: dsfsdf
deprecated: false
hidden: false
metadata:
  robots: index
---
Nix is a package manager designed to help you create reproducible and isolated builds. [JFrog Artifactory](/docs/artifactory) supports Nix repositories, enabling you to manage Nix packages and channels in a centralized location. By integrating with Nix, Artifactory acts as a high-performance binary cache (substituter), ensuring reliable, reproducible, and fast builds for your applications.


<Image src="https://files.readme.io/4b90fb754556ce8d3a764690a131609203a4c5bbb3402425113964e82ceb4c48-package_management_images_for_Nix_documentation.png" align="center" />


Artifactory fully supports Nix repositories and enhances the Nix ecosystem with the following capabilities:

- **Private Binary Storage**: Host and share your own Nix builds internally in local repositories.
- **Smart Proxying**: Proxy and cache the official Nix registry <Anchor target="_blank" href="https://search.nixos.org/packages">search.nixos.org</Anchor> with a remote repository to save bandwidth and ensure offline availability.
- **Unified Access**: Aggregate multiple repositories into a single virtual repository for simplified client configuration.
- **Global Distribution**: Use [Federated repositories](/docs/federated-repositories) to synchronize Nix artifacts across different geographic locations.
- **Metadata Calculation**: Calculate metadata for Nix packages to enable artifact management and search in Artifactory.
- **Cryptographic Signing**: Sign packages in your private binary cache so Nix clients can verify they came from Artifactory and weren't tampered with.

## Get Started with Nix

To get started working with Nix, complete the following main steps:

1. [Create a Nix repository](#create-a-nix-repository)
2. [Connect Nix to Artifactory](#connect-nix-to-artifactory)
3. [Deploy](#deploy-nix-packages) and [install](#install-nix-packages) Nix binaries and channels


<Image src="https://files.readme.io/c7a125e441f13230e25766e125552ef398b62c58b4191ec1fcf512a23f65787d-package_management__Nix_documentation.png" align="center" />


## Create a Nix Repository

This topic describes how to create a Nix repository. This is required before publishing and installing Nix packages and channels. There are three primary types of repositories:

- **Local repositories**: Store and share first- and second-party packages with your organization

- **Remote repositories**: Download packages from <Anchor target="_blank" href="https://search.nixos.org">search.nixos.org</Anchor> location and other Artifactory instances

- **Virtual repositories**: Aggregate remote and local repositories, enabling your organization to scale by providing a single URL that provides access to multiple repositories and types

For more information on JFrog repositories, see [Repository Management](/docs/repository-management).

**Prerequisite**: You need Admin or Project Admin permissions in Artifactory to create a repository. If you don't have Admin permissions, the option will not be available.

**To create a Nix repository**:

1. In the **Administration** tab, click **Repositories > Create a Repository**.

   ![CreateAnsibleLocal1.png](https://files.readme.io/689c36e9b67613873cac1a2e1a72ec4c529d081cfc5af182976e1f30ab854f45-uuid-45c813d9-16f6-c9f7-d1a1-4a86a4b1d6dd.png)
2. Select the type of repository you want to create.

   > 📘
   >
   > **Note**
   >
   > Artifactory supports federated Nix repositories.
3. Select the **Nix** package type.
4. Configure the required fields for the repository:

   - For local repositories, in the **Repository Key** field, type a meaningful name for the repository. For example, `nix-local`. For more information on local repositories and their settings, see [Local Repositories](/artifactory/docs/local-repositories).
   - For remote repositories, verify the **Repository URL** and update as needed. For more information on remote repositories and their settings, see <Anchor target="_blank" href="/artifactory/docs/remote-repositories#zapping-caches">Remote Repositories</Anchor>.
   - For virtual repositories, select one or more local or remote repository types to include in the virtual repository. For more information on virtual repositories and their settings, see <Anchor target="_blank" href="/artifactory/docs/virtual-repositories#select-repositories-to-include-in-a-virtual-repository">Virtual Repositories</Anchor>.
5. Click **Create Repository**. The repository is created and the Repositories window is displayed.

## Connect Nix to Artifactory

To use Nix with Artifactory, complete the following configurations as needed:

- [Configure Binary Cache](#configure-binary-cache)
- [Configure Channels](#configure-channels)

**Prerequisites:**

- Nix package manager installed on your local machine or build agent.
- A Nix repository. For more information, see [Create a Nix repository](#create-a-nix-repository).

### Configure Binary Cache

To use Artifactory as a binary cache instead of building from source, add it as a substituter in your `nix.conf` file.

**To add Artifactory as a substituter:**

1. Open the `nix.conf` file in a text editor from one of the following locations:
   - For user-specific configuration: `~/.config/nix/nix.conf`
   - For system-wide configuration: `/etc/nix/nix.conf`

     > 📘
     >
     > **Note**
     >
     > Editing system-wide configurations requires `root` or `sudo` admin privileges.
2. Add the following line to the `nix.conf` file:

   ```toml
   substituters = https://<USERNAME>:<AUTH>@<JFrogPlatformURL>/artifactory/api/nix/<REPO_NAME>?priority=<PRIORITY_VALUE>
   ```

   Where:

   - `<USERNAME>`: Your Artifactory username
   - `<AUTH>`: Your Artifactory identity token
   - `<JFrogPlatformURL>`: Your JFrog Platform URL
   - `<REPO_NAME>`: The name of the target repository
   - `<PRIORITY_VALUE>`: The query priority value

     > 📘
     >
     > **Note**
     >
     > Nix resolves dependencies based on priority. A lower value means a higher priority. The public cache <Anchor target="_blank" href="https://cache.nixos.org/">cache.nixos.org</Anchor> has a default priority of `40`. Set the Artifactory priority a value lower than `40` to make sure Artifactory is queried first.

   For example:

   ```toml
   substituters = https://jeffry:Random_Token218fwFughbreREAI5847fnf@company.jfrog.io/artifactory/api/nix/nix-local?priority=20
   ```
3. To enable modern CLI functionality, including the `nix copy` command to deploying packages, add the following snippet to the `nix.conf` file:
   ```toml
   experimental-features = nix-command
   ```
4. Save the changes to the file.
5. Reload the Nix daemon to apply the changes:
   ```shell
   sudo launchctl kickstart -k system/org.nixos.nix-daemon
   ```

<SetMeUpNote />

### Configure Channels

You can configure Nix repositories in Artifactory to proxy nixos channels or publish custom channels.

Publishing and caching channels in Artifactory provides a stable, versioned snapshot of the Nixpkgs ecosystem. The snapshots ensure that developers in your organization resolve dependencies against the same verified set of package expressions.

Using Artifactory to proxy and publish Nix channels safeguards build reproducibility and allows you to roll back or pin environments to specific channel releases even if upstream sources change or become unavailable.

**To configure channels to resolve from Artifactory:**

1. Run the following command:
   ```shell
   nix-channel --add https://<USERNAME>:<AUTH>@<JFrogPlatformURL>/artifactory/api/nix/<REPO_NAME>/channels/<CHANNEL_NAME> <CHANNEL_ALIAS>
   ```
   Where:
   - `<USERNAME>`: Your Artifactory username
   - `<AUTH>`: Your Artifactory identity token
   - `<JFrogPlatformURL>`: Your JFrog Platform URL
   - `<REPO_NAME>`: The name of the target repository
   - `<CHANNEL_NAME>`: The name of the Nix channel

     > 📘
     >
     > **Note**
     >
     > When working with a remote repository, the `<CHANNEL_NAME>` value must be an exact match for an official name in the <Anchor target="_blank" href="https://channels.nixos.org/">NixOS Channel Registry.</Anchor>
   For example:
   ```shell
   nix-channel --add https://jeffry:RandomToken_89786FRDSjkhgojrTUHwfeuh@company.jfrog.io/artifactory/api/nix/nix-remote/channels/nixpkgs-25.11-darwin 25.11-darwin
   ```
2. Save the changes to the file.
3. Run this command to update the Nix client:
   ```shell
   nix-channel --update
   ```

<SetMeUpNote />

**Next steps:**

- [Deploy Nix Packages](#deploy-nix-packages)
- [Install Nix Packages](#install-nix-packages)

## Deploy Nix Packages

You can perform two kinds of Nix deployments:

- Deploy Nix packages
- Deploy channel expressions

You can also [configure cryptographic signing](#configure-cryptographic-signing-for-nix-binary-caches) for local Nix repositories.

### Deploy Nix Packages

Use the nix copy command to push packages from your local store to Artifactory.

**To deploy Nix packages:**

- Run this command from the location in the directory that includes the `.nix` file:

  ```shell
  nix copy --to "https://<USERNAME>:<AUTH>@<JFrogPlatformURL>/artifactory/api/nix/<REPO_NAME>/" --file <PATH_TO_FILE>.nix
  ```

  Where:

  - `<USERNAME>`: Your Artifactory username
  - `<AUTH>`: Your Artifactory identity token
  - `<JFrogPlatformURL>`: Your JFrog Platform URL
  - `<REPO_NAME>`: The name of the target repository
  - `<PATH_TO_FILE>`: The path to the Nix package file on your local machine

  For example:

  ```shell
  nix copy --to "https://jeffry:Random_Token218fwFughbreREAI5847fnf@company.jrog.io/artifactory/api/nix/nix-local/" nix-package/default.nix
  ```

<SetMeUpNote />

### Deploy Channel Expressions

You can deploy a channel expression to Artifactory by using a curl `PUT` request.

> 📘
>
> **Note**
>
> The source file name must be named `nixexprs.tar.xz`. This name is mandatory and enforced. The Nix client specifically looks for this filename to resolve the channel expressions.

**To deploy a channel expression:**

- Run this command:

  ```shell
  curl -X PUT -u <USERNAME>:<AUTH> -T nixexprs.tar.xz https://<JFrogPlatformURL>/artifactory/api/nix/<REPO_NAME>/channels/<CHANNEL_NAME>/<NIX_FLAVOR>/<SNAPSHOT_IDENTIFIER>
  ```

  Where:

  - `<USERNAME>`: Your Artifactory username
  - `<AUTH>`: Your Artifactory identity token
  - `<JFrogPlatformURL>`: Your JFrog Platform URL
  - `<REPO_NAME>`: The name of the target repository
  - `<CHANNEL_NAME>`: The name of the channel
  - `<NIX_FLAVOR>`: The distribution or flavor of Nix. Potential values are:
    - `nixpkgs`
    - `nixos`
  - `<SNAPSHOT_IDENTIFIER>`: The snapshot identifier

  For example:

  ```shell
  nix copy --to "https://jeffry:Random_Token218fwFughbreREAI5847fnf@company.jrog.io/artifactory/api/nix/nix-local/" nix-package/default.nix
  ```

<SetMeUpNote />

## Install Nix Packages

You can install Nix packages from Artifactory using one of the following supported methods:

- [`nix-env`](#install-nix-packages-with-nix-env)
- [`nix-shell`](#install-nix-packages-with-nix-shell)
- [NixOS Configuration](#install-nix-packages-with-nixos-configuration)

### Install Nix Packages with nix-env

**To install Nix packages with&#x20;**`nix-env`:

- Run the following command:
  ```shell
  nix-env -iA nixpkgs.<PACKAGE_NAME>
  ```
  Where `<PACKAGE_NAME>` is the name of the Nix package. For example:
  ```shell
  nix-env -iA nixpkgs.neovim
  ```

### Install Nix Packages with nix-shell

**To install Nix packages with&#x20;**`nix-shell`**:**

- Run the following command:
  ```shell
  nix-shell -p <PACKAGE_NAME>
  ```
  Where `<PACKAGE_NAME>` is the name of the Nix package. For example:
  ```shell
  nix-shell -p neovim
  ```

### Install Nix packages with NixOS Configuration

**To install Nix packages with NixOS Configuration:**

1. Open the `/etc/nixos/configuration.nix` file in a text editor.
2. Add the following snippet to the file:

   ```js
   environment.systemPackages = [ 
       pkgs.<PACKAGE_NAME>
   ];
   ```

   Where `<PACKAGE_NAME>` is the name of the Nix package. For example:

   ```js
   environment.systemPackages = [ 
       pkgs.neovim
   ];
   ```
3. Save the changes to the file.

## Additional Nix Information

The following topics provide additional information about working with Nix repositories in Artifactory.

- [Configure Cryptographic Signing for Nix Binary Caches](#configure-cryptographic-signing-for-nix-binary-caches)
- [Nix Package Identification](#nix-package-identification)
- [Best Practices for Nix Naming and Versioning](#best-practices-for-nix-naming-and-versioning)
- [Nix Authentication](#nix-authentication)

### Configure Cryptographic Signing for Nix Binary Caches

When you use Artifactory as a private Nix binary cache, cryptographic signing helps your build agents and developers trust the packages they download. Nix verifies each package against a public key you configure on the client, so substitutes are accepted only when they match what your organization signed.

Once you assign a signing key to a local Nix repository, Artifactory signs packages automatically when they're deployed or downloaded. You don't need a separate publish command or extra flags.

Complete the following tasks to enable signed binary caches:

1. [Configure Ed25519 Signing in Artifactory](#configure-ed25519-signing-in-artifactory)
2. [Configure Nix Client Trusted Public Keys](#configure-nix-client-trusted-public-keys)

#### Configure Ed25519 Signing in Artifactory

**Prerequisite**: You need Admin or Project Admin permissions to manage keys and repository settings. For more information, see [Manage Signing Keys](/administration/docs/security-keys-management).

**To configure Ed25519 signing for a Nix local repository:**

1. Generate an Ed25519 key pair on your machine:

   ```shell
   openssl genpkey -algorithm Ed25519 -out ed25519-private.pem
   openssl pkey -in ed25519-private.pem -pubout -out ed25519-public.pem
   ```

2. In the **Administration** module, go to **Platform Security** > **Keys Management**.

3. Click **Add Keys**, and select **Ed25519 Keys** from the dropdown list.

4. Enter a name and alias for the key pair, and upload the public and private key files.

5. Click **Add Ed25519 Key**.

6. In the **Administration** module, go to **Repositories** and select your local Nix repository.

7. In the **Basic** tab of the repository settings, under **Ed25519 Key Pair**, select the key you created from the **Primary Key Name** list.

8. Click **Save**.

> 📘
>
> **Note**
>
> Use the same alias on the key pair and in your Nix client `trusted-public-keys` configuration.

Deploy packages with the standard [`nix copy`](#deploy-nix-packages) workflow. Artifactory handles signing for you.

#### Configure Nix Client Trusted Public Keys

Nix only accepts signed substitutes from caches whose public keys you trust. Add your Artifactory signing key to `nix.conf` so builds can use your private binary cache.

**To configure the Nix client to verify Artifactory signatures:**

1. Open the `nix.conf` file from one of the following locations:
   - For user-specific configuration: `~/.config/nix/nix.conf`
   - For system-wide configuration: `/etc/nix/nix.conf`

2. Add or update the `trusted-public-keys` setting with your Artifactory key entry:

   ```toml
   trusted-public-keys = <EXISTING_KEYS> <KEY_ALIAS>:<BASE64_PUBLIC_KEY>
   ```

   Where:

   - `<EXISTING_KEYS>`: Any existing trusted keys you want to keep, such as the official NixOS cache key
   - `<KEY_ALIAS>`: The alias of the Ed25519 key pair assigned to your Nix repository
   - `<BASE64_PUBLIC_KEY>`: The public key value for that alias

   For example:

   ```toml
   trusted-public-keys = cache.nixos.org-1:6NCHdBS49z37Hr9WSDLXOrT2q8x5mA5kE48fRA2zIDQ= my-nix-cache-1:cNpfNfHQEZ+rzOkvB985IKlWFT4nxl+G3HwxV6t92EY=
   ```

3. Save the changes to the file.

4. Reload the Nix daemon to apply the changes:

   ```shell
   sudo launchctl kickstart -k system/org.nixos.nix-daemon
   ```

<SetMeUpNote />

**Next steps:**

- [Deploy Nix Packages](#deploy-nix-packages)
- [Configure Binary Cache](#configure-binary-cache)

### Nix Package Identification

This section provides information on how Artifactory identifies and presents Nix package information. Artifactory provides native support for caching and aggregating Nix packages.

Artifactory follows a best-effort aggregation model when presenting packages and versions in the UI and APIs. This means that instead of exposing every build artifact as a separate package, Artifactory groups related artifacts together to provide a more natural browsing and discovery experience. This approach balances typical package searching workflows with Nix system compatibility.

#### How Artifactory Identifies Nix Packages

To identify and group packages, Artifactory extracts the following package metadata from the Nix `narInfo` metadata:

- The Nix store path (`storePath`)
- The name and version encoded in that path

This information populates the Packages view, where you can browse packages by name, see how many versions are available, and identify the latest available version. For more information, see [Viewing Packages](/docs/viewing-packages).

> 📘
>
> **Note**
>
> The Packages page is designed for browsing available packages, understanding what software exists in a repository, identifying commonly used versions, and high-level visibility across repositories.
>
> It is not intended to replace Nix's native mechanisms for reproducible builds, dependency planning, or cryptographic identity guarantees.

#### Why Store Hash Isn't the Primary Package Identity

Nix packages are fundamentally content-addressed. Each build output has a unique store path hash derived from all of its inputs. While this guarantees correctness and reproducibility, using the store hash as the primary identity would have significant drawbacks for aggregation in Artifactory:

- Every rebuild, even with minimal changes, would appear as a new package
- The number of visible packages would grow exponentially
- Significant negative impacts on discoverability
- Browsing by “logical package” (for example, Firefox) would be impractical

Because of these implications, Artifactory does not treat each store hash as a separate package entry. Instead, the system groups artifacts using the extracted name and version information to provide a usable catalog.

### Best Practices for Nix Naming and Versioning

The following are best practices when publishing Nix packages with full control over naming and versioning:

- Use a stable and explicit package name.
- Avoid toolchain or runtime identifiers in the name.
- Use clean and predictable version string.
- Where possible, use semantic versioning.
- Avoid embedding branch names, dates, or commit hashes directly in the version.
- Encode build or revision metadata separately.
- Maintain consistent naming across releases.

These practices are recommended to improve aggregation accuracy and discoverability in Artifactory.

### Nix Authentication

The Nix client does not provide interactive authentication prompts. To authenticate with Artifactory, you must provide credentials using one of the following methods:

- **Credentials in URL (Recommended)**: Embed credentials directly in the repository URL using the format `https://<USERNAME>:<AUTH>@<JFrogPlatformURL>/<REPO_NAME>`.
- `.netrc`**&#x20;File**: Add your Artifactory credentials to `~/.config/nix/nix.conf` or `/etc/nix/nix.conf` to authenticate to Artifactory as a binary.
- `access-tokens`: Pass authentication against APIs when performing fetch operations like `fetchTarball` or `fetchurl` from a `.nix` file.
  - CLI:
    ```shell
    nix build . --option access-tokens "github.com=$<GITHUB_TOKEN>"
    ```
  - In `nix.conf`:

    ```toml
    access-tokens = github.com=ghp_<TOKEN> gitlab.com=glpat_<TOKEN>
    ```
  To authenticate to Artifactory as a binary cache or for generic file hosting, you still need to use the `.netrc` method.

## Nix Limitations in Artifactory

The following are the limitations of Nix repositories in Artifactory:

- **Registry Browsing**: Artifactory doesn't support browsing the contents of remote Nix registries via UI. Only artifacts that have been explicitly pulled or deployed will appear in the artifact tree.
- **Authentication**: The Nix client does not provide interactive authentication prompts. For more information about authentication options, see [Nix Authentication](#nix-authentication).
- **Version extraction**: The following are limitations related to Nix package version extraction.
  - **Free-form version strings**: Nix does not enforce a strict versioning standard. Version strings may include numbers, dates, channel or branch identifiers, or Git-derived identifiers. Free-form versioning has the following impact on Nix packages in Artifactory:
    - Versions may not follow semantic versioning
    - Version ordering may not reflect chronological or functional precedence
    - The "latest version” is best-effort metadata, not an authoritative identifier
  - **Duplicate or ambiguous versions**: In cases of duplicate or ambiguous versions, Artifactory aggregates packages based on the extracted version value and does not attempt to differentiate further at the package level.

    Examples of duplicate or ambiguous versions are the same version string appearing multiple times, different builds with the same extracted version, or patch-level changes that are indistinguishable at the version string level.
- **Name extraction**: The displayed package name may not match the name used with `nix install` for the following reasons.
  - **Toolchain and runtime prefixes**: The extracted package name may include store path prefixes from language-based or toolchain-based build tools.
  - **Package name overrides**: Some Nix derivations explicitly override the package name (`pname`) value during evaluation, and the store path may still reflect intermediate or contextual naming.

<br />
