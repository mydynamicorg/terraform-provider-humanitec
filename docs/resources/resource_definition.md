---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "humanitec_resource_definition Resource - terraform-provider-humanitec"
subcategory: ""
description: |-
  Visit the docs https://docs.humanitec.com/reference/concepts/resources/definitions to learn more about resource definitions.
---

# humanitec_resource_definition (Resource)

Visit the [docs](https://docs.humanitec.com/reference/concepts/resources/definitions) to learn more about resource definitions.

## Example Usage

```terraform
resource "humanitec_resource_definition" "s3" {
  id   = "s3-dev-bucket"
  name = "s3-dev-bucket"
  type = "s3"

  driver_type = "humanitec/s3"
  driver_inputs = {
    values = {
      region = "us-east-1"
     
     criteria = [
    {
      app_id   = "my-app",
      env_type = "development",
      res_id   = "shared.logs-dns"
    }
  ]
    }
  }
}

resource "humanitec_resource_definition" "postgres" {
  id          = "db-dev"
  name        = "db-dev"
  type        = "postgres"
  driver_type = "humanitec/postgres-cloudsql-static"

  driver_inputs = {
    values = {
      "instance" = "test:test:test"
      "name"     = "db-dev"
      "host"     = "127.0.0.1"
      "port"     = "5432"
    }
    secrets = {
      "username" = "test"
      "password" = "test"
    }
  }
}

resource "humanitec_resource_definition" "gke" {
  id          = "gke-dev"
  name        = "gke-dev"
  type        = "k8s-cluster"
  driver_type = "humanitec/k8s-cluster-gke"

  driver_inputs = {
    values = {
      "loadbalancer" = "1.1.1.1"
      "name"         = "gke-dev"
      "project_id"   = "test"
      "zone"         = "europe-west3"
    }
    secrets = {
      "credentials" = "{}"
    }
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `driver_type` (String) The driver to be used to create the resource.
- `id` (String) The Resource Definition ID.
- `name` (String) The display name.
- `type` (String) The Resource Type.

### Optional

- `criteria` (Attributes Set) The criteria to use when looking for a Resource Definition during the deployment. (see [below for nested schema](#nestedatt--criteria))
- `driver_account` (String) Security account required by the driver.
- `driver_inputs` (Attributes) Data that should be passed around split by sensitivity. (see [below for nested schema](#nestedatt--driver_inputs))

<a id="nestedatt--criteria"></a>
### Nested Schema for `criteria`

Optional:

- `app_id` (String) The ID of the Application that the Resources should belong to.
- `env_id` (String) The ID of the Environment that the Resources should belong to. If env_type is also set, it must match the Type of the Environment for the Criteria to match.
- `env_type` (String) The Type of the Environment that the Resources should belong to. If env_id is also set, it must have an Environment Type that matches this parameter for the Criteria to match.
- `res_id` (String) The ID of the Resource in the Deployment Set. The ID is normally a . separated path to the definition in the set, e.g. modules.my-module.externals.my-database.

Read-Only:

- `id` (String) Matching Criteria ID


<a id="nestedatt--driver_inputs"></a>
### Nested Schema for `driver_inputs`

Optional:

- `secrets` (Map of String, Sensitive) Secrets section of the data set.
- `values` (Map of String) Values section of the data set. Passed around as-is.


