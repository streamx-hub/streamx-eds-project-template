# streamx-eds-template
This repository provides a template for quickly setting up a project using **Edge Delivery Services** with **StreamX**.

Before running the project, make sure to replace all required placeholders in properties files in the `config` directory.
The placeholders are marked with `<REQUIRED_VALUE>` token.

## Required Properties

 - `streamx.cloud.project-id` - Your StreamX Cloud project ID
 - `streamx.eds-base.url` - The base URL of the EDS site, used by the mesh services to retrieve resources

## GitHub Workflows

For details, see the workflows [`README.md`](.github/workflows/README.md)  file.