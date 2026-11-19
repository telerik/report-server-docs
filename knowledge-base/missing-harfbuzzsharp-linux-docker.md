---
title: Resolving Missing HarfBuzzSharp in Linux Containers
page_title: Fix Missing libHarfBuzzSharp.so in Report Server for .NET on Linux
description: "Resolve native HarfBuzzSharp load errors in Telerik Report Server for .NET Linux containers with the matching Linux native-assets package."
type: troubleshooting
slug: missing-harfbuzzsharp-linux-docker
tags: report-server,dotnet,docker,linux,harfbuzz,skia,arabic,pdf
res_type: kb
---

# Resolving Missing HarfBuzzSharp in Linux Containers

## Environment

The following environment applies to the verified image contents:

| Property | Value |
|---|---|
| Product | Telerik Report Server for .NET |
| Deployment | Linux Docker container, including Azure Container Apps |
| Architecture | `linux/amd64`, also reported as `x86_64` |
| Graphics engine | Skia |
| Image repository | `progressofficial/telerik-reportserver-app` |
| Affected image tags verified | `12.2.26.1008` and `12.3.26.1111` |

## Description

A report operation fails with a native library load error. The exception includes messages similar to the following:

```text
Unable to load shared library 'libHarfBuzzSharp' or one of its dependencies.
/app/runtimes/linux-x64/native/libHarfBuzzSharp.so:
cannot open shared object file: No such file or directory
```

The application can start and display its web interface without this error. The failure occurs when a report operation calls the affected text-processing code.

HarfBuzz provides text shaping, which maps text to positioned glyphs. Complex scripts, such as Arabic, can require this process. PDF export is one operation to test.

An Arabic-capable font and the native HarfBuzzSharp library serve different purposes. A font supplies glyphs; HarfBuzz shapes text. An installed font does not replace `libHarfBuzzSharp.so`.

The error does not establish that every Arabic report or every PDF export fails.

## Cause

The RS.NET Linux docker images contain the managed assemblies `HarfBuzzSharp.dll` and `SkiaSharp.HarfBuzz.dll`, but omit the Linux native file `libHarfBuzzSharp.so`. Linux cannot use the Windows or macOS native assets in those images.

The following table summarizes the verified image contents:

| Image tag | Linux x64 native file |
|---|---|
| `12.1.26.708` | Present |
| `12.2.26.1008` | Missing |
| `12.3.26.1111` | Missing |

These results identify a packaging difference between the inspected releases.

In the 2026 Q3/Q4 images, the application dependency manifest references [HarfBuzzSharp/8.3.1.2](https://www.nuget.org/packages/HarfBuzzSharp/8.3.1.2#dependencies-body-tab), but does not list `HarfBuzzSharp.NativeAssets.Linux`.

The Docker images use the prebuilt NonWindows distribution. The file `libHarfBuzzSharp.so` is absent from that distribution.

## Solution

Build a custom image that includes the Linux native asset from the package version that matches the managed HarfBuzzSharp dependency.

> important The following workaround targets the verified Q4 Linux x64 image and `HarfBuzzSharp` version `8.3.1.2`. Do not reuse the older native file from `12.1.26.708` or replace managed assemblies.

### Checking the Deployed Image

Identify the image reference and digest for the container that reports the exception. In Azure Container Apps, inspect the affected revision rather than a different revision or the current `latest` tag.

Use the Azure console for Azure Container Apps. Use `docker exec` only for containers that the selected Docker daemon manages.

#### Inspecting Azure Container Apps

Open a shell in the affected application container through the [Azure Container Apps console](https://learn.microsoft.com/en-us/azure/container-apps/container-console#azure-portal):

1. In the Azure portal, open the container app and select **Console** under **Monitoring**.
2. Select the affected revision, replica, and application container.
3. Select **sh** to start `/bin/sh`.

Run the following commands inside that shell:

```sh
find /app -name libHarfBuzzSharp.so -print
cat /app/Telerik.ReportServer.Web.Core.deps.json
```

In the manifest's `libraries` section, locate the `HarfBuzzSharp/<version>` entry. For the verified Q4 image, the file search returns no match and the manifest lists `HarfBuzzSharp/8.3.1.2`.

If the native file exists, check the relevant Linux x64 file returned by `find` in the same shell. Replace `FOUND_PATH` with the file's full path:

```sh
ldd "FOUND_PATH"
```

Run these commands without a `docker exec` wrapper. Resolve dependencies marked `not found` in the final runtime image. Verify the architecture and whether the image uses glibc or musl.

#### Inspecting Containers Through Docker

Run the following PowerShell commands on the Docker host. Replace `YOUR_CONTAINER` with the container name:

```powershell
docker exec YOUR_CONTAINER /bin/sh -c 'find /app -name libHarfBuzzSharp.so -print'

docker exec YOUR_CONTAINER /bin/sh -c 'cat /app/Telerik.ReportServer.Web.Core.deps.json' |
    ConvertFrom-Json |
    ForEach-Object {
        $_.libraries.PSObject.Properties.Name |
            Where-Object { $_ -like 'HarfBuzzSharp/*' }
    }
```

For the verified Q4 image, the first command returns no file and the second returns `HarfBuzzSharp/8.3.1.2`.

If the native file exists, check the system dependencies of the relevant Linux x64 file returned by `find`. Do not assume this packaging issue applies. Replace `FOUND_PATH` with the file's full path:

```powershell
docker exec YOUR_CONTAINER /bin/sh -c 'ldd "FOUND_PATH"'
```

Resolve dependencies marked `not found` in the final runtime image. Also verify the architecture and whether the image uses glibc or musl.

### Building a Custom Image

Use Docker in Linux container mode. The following commands run in PowerShell on the host, not inside the application container.

For a customized Q4 deployment, use the inspected deployed image as the base to preserve its fonts, drivers, and configuration. For a published image, pin its registry digest. A stock Q4 base does not retain those customizations.

Before the build, verify the managed HarfBuzzSharp version with the manifest check above. Use package version `8.3.1.2` only if that version matches the deployed managed dependency.

An image that exists only on the Docker host, such as `telerik-report-server:local`, has no published registry digest. Do not run `docker pull` for that local-only image.

For an already-published image, including an Azure Container Apps deployment, use the affected deployment's image repository reference and digest. Continue with the runtime-user check below. Skip the following container inspection, tag, and push commands.

If the deployed image exists only on a Docker host, first publish that exact image to a private registry. Authenticate to that registry, then run the following commands on that host. Replace `YOUR_CONTAINER` and `YOUR_REGISTRY` with your container name and registry hostname:

```powershell
$deployedImageId = docker inspect YOUR_CONTAINER --format '{{.Image}}'
docker tag $deployedImageId YOUR_REGISTRY/reportserver-base:harfbuzz-workaround
docker push YOUR_REGISTRY/reportserver-base:harfbuzz-workaround
```

For this local-only image flow, use the reference and digest reported by `docker push` as the published base image. The reference has the form `YOUR_REGISTRY/reportserver-base@sha256:DIGEST`.

Also verify the base image's configured runtime user. For a published image, authenticate to its registry, then run the following commands. Replace `YOUR_DEPLOYED_IMAGE` with its repository reference and digest:

```powershell
docker pull YOUR_DEPLOYED_IMAGE
docker image inspect YOUR_DEPLOYED_IMAGE --format '{{json .Config.User}}'
```

An empty user value means the image defaults to `root`. Preserve any deployment-level user override when you redeploy.

1. In a new, empty working folder, download and extract the matching [HarfBuzzSharp.NativeAssets.Linux package](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/8.3.1.2):

   ```powershell
   Invoke-WebRequest `
       'https://api.nuget.org/v3-flatcontainer/harfbuzzsharp.nativeassets.linux/8.3.1.2/harfbuzzsharp.nativeassets.linux.8.3.1.2.nupkg' `
       -OutFile 'harfbuzz.zip'

   Expand-Archive -Path '.\harfbuzz.zip' -DestinationPath '.\harfbuzz'
   ```

2. Create a file named `Dockerfile` in that folder. The following example uses the stock Q4 Linux x64 image:

   ```dockerfile
   FROM progressofficial/telerik-reportserver-app@sha256:e8425c1ae19564c2434fbac05f389ef53f37876f64a3917d3d7550085b83eef2

   USER root
   COPY harfbuzz/runtimes/linux-x64/native/libHarfBuzzSharp.so /app/runtimes/linux-x64/native/libHarfBuzzSharp.so
   RUN chmod 644 /app/runtimes/linux-x64/native/libHarfBuzzSharp.so
   USER app
   ```

   For a customized deployment, replace the `FROM` reference with your inspected deployed image and digest. Replace the final `USER app` instruction with that base image's original user value, including any group. Use `USER root` if the original value is empty.

   The stock image uses `app`. The final `USER` instruction restores the base image's runtime user after the file copy.

3. Build the image with the following command:

   ```powershell
   docker build --platform linux/amd64 -t reportserver-harfbuzz:12.3.26.1111 .
   ```

4. Verify the file and its system dependencies with the following command:

   ```powershell
   docker run --rm --entrypoint /bin/sh reportserver-harfbuzz:12.3.26.1111 `
       -c 'ls -l /app/runtimes/linux-x64/native/libHarfBuzzSharp.so && ldd -r /app/runtimes/linux-x64/native/libHarfBuzzSharp.so'
   ```

   Confirm that the file exists and the output contains no missing libraries or unresolved symbols.

### Deploying and Validating the Image

For a local deployment, update the application image in your Compose configuration. For Azure Container Apps, publish the custom image to an accessible registry.

The following PowerShell commands publish the image. Replace `YOUR_REGISTRY` with your registry hostname and authenticate to that registry first:

```powershell
docker tag reportserver-harfbuzz:12.3.26.1111 YOUR_REGISTRY/reportserver-harfbuzz:12.3.26.1111
docker push YOUR_REGISTRY/reportserver-harfbuzz:12.3.26.1111
```

Complete the deployment and validation steps:

1. Update the application to use the custom image. Preserve the existing license, encryption keys, environment variables, secrets, and database configuration.
2. Restart or redeploy the application. In Azure Container Apps, verify the new revision and route test traffic to that revision.
3. Confirm that no volume mount hides `/app/runtimes/linux-x64/native/libHarfBuzzSharp.so`.
4. Repeat the original failing report operation and inspect the [application logs](slug:logging-rs-net).

For an Arabic text test, use an Arabic-capable font, such as `Noto Naskh Arabic`, that is available in the container. Preview the report and export it to PDF. The native-file workaround does not install fonts.

> important A successful application startup does not validate report rendering. Verify the affected report before you direct production traffic to the new revision.

Do not rely on a manual copy into a live container as a persistent fix. Container replacement removes that change unless the image or deployment configuration includes the file.

## See Also

Related documentation includes:

- [Installing Report Server for .NET in Containers](slug:dotnet-installation-on-docker-container).
- [Installing RS.NET on Docker Container with Custom Image](slug:custom-image-dotnet-installation-on-docker-container).
- [Logging in Report Server for .NET](slug:logging-rs-net).
- [HarfBuzzSharp.NativeAssets.Linux 8.3.1.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/8.3.1.2).
