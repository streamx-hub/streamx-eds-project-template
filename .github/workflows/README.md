# STREAMX-EDS-TEMPLATE · GitHub Workflows

## Quick Start

Follow these steps to quickly set up and publish your project to **StreamX**:

1. **Set up repository secrets**
    - Add `STREAMX_INGESTION_EDS_TOKEN` (ask your StreamX admin).
    - Add `STREAMX_INGESTION_TOKEN` (ask your StreamX admin).

2. **Configure repository variables**
    - `EDS_DOMAIN_URL` → DA live endpoint (e.g.,
      `https://<branch>--<project_id>--<organization_id>.aem.live`).
    - `STREAMX_INGESTION_URL` → Hostname from StreamX admin.
    - `STREAMX_INGESTION_INCLUDES` → List of web resources.

3. **Run initial publish**
    - Trigger **Sync web resources with StreamX** workflow from GitHub Actions.
    - Use the **Crawl Tree** and **Bulk Operations** DA apps to publish content resources.

✅ Done! Your web resources and content are now available in **StreamX**.

---

## Overview

This repository provides GitHub Actions workflows to **ingest and synchronize data from EDS into
StreamX**.  
These workflows automate publishing, unpublishing, and syncing of web and content resources,
ensuring that StreamX always has the latest project state.

---

## Workflows

The following GitHub Actions workflows are required:

- [`publish-to-streamx.yaml`](.github/workflows/publish-to-streamx.yaml)  
  Triggered when a page or content resource is published from the DA console.

- [`unpublish-from-streamx.yaml`](.github/workflows/unpublish-from-streamx.yaml)  
  Handles unpublishing of resources that were previously ingested into StreamX.

- [`webresource-sync-with-streamx.yaml`](.github/workflows/webresource-sync-with-streamx.yaml)  
  Synchronizes or triggers the initial load of all web resources stored in the repository (ref:
  Arbory-Dev repository).

---

## GitHub Actions Configuration

### Secrets

| Key                           | Value              | Description                                              | 
|-------------------------------|--------------------|----------------------------------------------------------|
| `STREAMX_INGESTION_EDS_TOKEN` | `<REQUIRED_VALUE>` | Contact your StreamX administrator to obtain this token. |
| `STREAMX_INGESTION_TOKEN`     | `<REQUIRED_VALUE>` | Contact your StreamX administrator to obtain this token. |

### Variables

| Key                          | Example Value                                                                                      | Description                                                |
|------------------------------|----------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `EDS_DOMAIN_URL`             | `https://<branch>--<project_id>--<organization_id>.aem.live`                                       | Hostname of the DA live endpoint.                          |
| `STREAMX_INGESTION_URL`      | `https://<streamx_processing_hostname_prefix>.streamx.cloud`                                       | Ingestion hostname provided by your StreamX administrator. |
| `STREAMX_INGESTION_INCLUDES` | `["blocks/**", "fonts/*", "icons/*", "scripts/**", "styles/*", "helix-query.yaml", "favicon.ico"]` | List of web resources relevant for the hosted DA project.  |

For details, see
the [StreamX Connector GitHub specification](https://github.com/streamx-dev/streamx-common-github-actions?tab=readme-ov-file#create-streamx-connector-github-action).

---

## Initial Publish

Once workflows and secrets/variables are configured, you can trigger the **initial publish of all
content and web resources into StreamX**.

This process involves two steps:

1. Publish project **web resources**
2. Publish project **content resources**

---

### 1. Publishing Web Resources

Use the **Sync with StreamX** workflow:

1. Go to the **GitHub Actions** tab.
2. Select **Sync web resources with StreamX** workflow.
3. Open the **Run workflow** dropdown (top-right).
    - Choose the branch (e.g., `main`).
    - Enable the option: *“Publish all pattern-included web resources to StreamX”*.
4. Click **Run workflow**.
5. Wait for execution to finish and verify successful publishing.

---

### 2. Publishing Content Resources

Publishing content requires **DA apps** (Crawl Tree & Bulk Operations) alongside the DA console.

#### Step A · Collect content resources with [Crawl Tree](https://da.live/apps/tree)

1. Open **Crawl Tree** app.
2. Enter the root content path: `/organization_id/project_id`.
3. Click **Crawl** and wait for results.
4. Switch to **absolute path view** with the *Toggle view* button.
5. Click **Copy list** to copy the resource paths.

#### Step B · Publish with [Bulk Operations](https://da.live/apps/bulk)

1. Open **Bulk Operations** app.
2. Paste the copied content paths.
3. Select **Publish** from the dropdown.
4. Click **Submit**.
5. Monitor progress in the **Publish to StreamX** workflow logs.

---

✅ After these steps, all project web and content resources will be available in **StreamX**.  
