# Deployer

A small Windows app for deploying with Flux CD: it lists the Deployments in a GitLab deployments repo with their image tags, lets you pick a new tag from the GitLab container registry, and commits the change to the branch Flux watches.

**[Download Deployer.exe](https://github.com/NikolaCunovic/deployer-releases/releases/latest/download/Deployer.exe)** (Windows 10 and 11, always the newest version)

## What it does

- Lists every Deployment (and StatefulSet / DaemonSet) in a folder of the repo, grouped by app folder, with each container's image and tag.
- Click a tag to pick another one from the GitLab container registry, or type one.
- Changes several apps at once and shows exactly what will change (a diff of each `image:` line) before committing them all in one commit.
- Changes only the tag. The rest of each file stays exactly as it was.
- See each app's past deploys (tag, date, who, commit) and roll back to one in two clicks.
- Won't overwrite anyone: if a file changed on the branch since you loaded the list, it stops and asks you to refresh.
- One connection per cluster, switched from the top bar. Mark production as **Protected** to make every deploy there ask for its name.
- Updates itself: when a new version is out, a green **Update to …** button appears at the top.

## Install

1. Download **Deployer.exe**. If your browser says the file "isn't commonly downloaded", choose **Keep**.
2. Put it in a folder where it can stay, for example `C:\Users\<you>\Apps\Deployer\`.
3. Run it. Windows may show **"Windows protected your PC"**: click **More info**, then **Run anyway**. This appears because the app isn't signed with a paid certificate.
4. In GitLab, create a personal access token (**Preferences › Access tokens**) with the scopes **api** and **read_registry**.
5. In Deployer, choose **Add connection**: a name (for example Test), your GitLab address, the deployments project, the branch, and the folder that holds the manifests. Paste the token and click **Test**.

## Your data stays on your PC

- Connections: `%APPDATA%\Deployer\settings.json`.
- Your GitLab token: Windows Credential Manager, never in a file.
- The app talks only to your GitLab, and to GitHub to check for a new version (nothing about you is sent). There's no account, cloud or tracking.

## Updating

Deployer checks for a new version when it starts and every few hours. When one is out, click **Update to …** at the top and choose **Update and restart**; your connections and token are kept. You can also check in **Settings**, bottom left.

If updating doesn't work: close Deployer, replace `Deployer.exe` with the new download, and start it again.

## Requirements

Windows 10 or 11 with the Microsoft Edge WebView2 Runtime, which Windows 11 and up-to-date Windows 10 already include.
