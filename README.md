# StreamX + Edge Delivery Services Template

This repository provides a **template project for integrating StreamX with Edge Delivery Services (EDS)**.

The integration allows **Edge Delivery Services to act as the primary content source**, while **StreamX handles ingestion, delivery, and search indexing**.

All pages and assets published from EDS are automatically ingested into StreamX and can be delivered through **StreamX services alongside the Edge Delivery CDN**.

Additionally, the template includes **OpenSearch**, which indexes all ingested pages to enable search capabilities across the delivered content.

---

# Architecture Overview

The system architecture works as follows:

1. **Edge Delivery Services (EDS)** acts as the primary content source.
2. When content is published from EDS:

   * Pages and assets are ingested into **StreamX**
   * The content becomes available through **StreamX delivery services**
3. **OpenSearch** indexes all ingested pages.
4. Content is delivered through:

   * **Edge Delivery CDN**
   * **StreamX**

```
EDS (Content Source)
        │
        │ publish
        ▼
   StreamX Ingestion
        │
        ├── Content Delivery
        │
        └── OpenSearch Indexing
```

---

# Prerequisites

Before starting the setup ensure you have:

* An existing **Edge Delivery Services (EDS) project**
* A **StreamX project created from this repository**
* Access to the **StreamX Console**

---

# EDS Repository Configuration

Your **Edge Delivery Services repository** must be configured to allow synchronization of frontend resources with StreamX.

Add the following **environment variables** to the repository configuration.

---

## STREAMX_INGESTION_INCLUDES

Defines the list of file patterns that should be synchronized with StreamX.

Example:

```
STREAMX_INGESTION_INCLUDES=[
  "blocks/**",
  "components/**",
  "fonts/**",
  "icons/**",
  "images/**",
  "scripts/*.js",
  "styles/*.css",
  "libs/**",
  "templates/**",
  "helix-query.yaml"
]
```

These paths define which **frontend resources** will be ingested into StreamX.

---

## STREAMX_INGESTION_GH_TOKEN

Token used by the GitHub workflows to authenticate with StreamX.

You can retrieve the token from the **StreamX Console**:

```
Sources → GitHub
```

Then configure it in your repository:

```
STREAMX_INGESTION_GH_TOKEN=<TOKEN>
```

---

## STREAMX_INGESTION_URL

Use the ingestion URL obtained from the **Rest Ingestion Gateway** in the StreamX Console.

```
STREAMX_INGESTION_URL=<REST_INGESTION_URL>
```

---

# GitHub Workflows

This template provides **two GitHub workflows** responsible for synchronizing resources and content between EDS and StreamX.

Both workflows can be found in:

```
github-action/
```

They must be copied into your EDS repository:

```
.github/workflows/
```

---

# Workflow 1 — Full Repository Sync

This workflow performs a **full synchronization of frontend resources** from the EDS repository into StreamX.

It is typically used:

* During **initial setup**
* When performing **manual re-synchronization**

### Workflow Name

```
StreamX Full Code Sync
```

### How to Run

1. Go to **GitHub Actions**
2. Select:

```
StreamX Full Code Sync
```

3. Click **Run workflow**
4. Choose the branch you want to synchronize.

The workflow will ingest all resources defined in:

```
STREAMX_INGESTION_INCLUDES
```

---

# Workflow 2 — EDS Publish Sync

This workflow handles **content published through Edge Delivery Services**.

Whenever new content is published in EDS:

* The content is **ingested into StreamX**
* The pages are **indexed in OpenSearch**
* Updated content becomes available through **StreamX delivery services**

### Workflow Name

```
StreamX EDS Publish Sync
```

### Trigger

This workflow runs automatically when:

* Content is **published through Edge Delivery Services**

It ensures that **new or updated content is immediately synchronized with StreamX**.

---

# Searching Indexed Pages

All pages ingested from **Edge Delivery Services (EDS)** are automatically indexed in **OpenSearch**.

This allows searching through the delivered content using the built-in search endpoint.

You can query indexed pages using the following path:

```
/search/pages?query=YOUR_QUERY
```

### Example

```
/search/pages?query=homepage
```

This endpoint returns pages that match the provided search query based on the **OpenSearch index** created during ingestion.

### Search Flow

1. Content is published in **Edge Delivery Services**
2. The content is ingested into **StreamX**
3. Pages are indexed in **OpenSearch**
4. The search endpoint returns matching results

```
EDS Publish
     │
     ▼
StreamX Ingestion
     │
     ▼
OpenSearch Index
     │
     ▼
/search/pages?query=YOUR_QUERY
```

---

# Result

After completing the setup:

* Frontend resources from the **EDS repository** are synchronized with **StreamX**
* All pages are **indexed in OpenSearch**
* Content can be delivered through:

   * **Edge Delivery CDN**
   * **StreamX Delivery Services**

---