---
layout: default
title: Kibana Multi-Tenancy
parent: Access Control
grand_parent: Security
nav_order: 30
---

# Kibana multi-tenancy

*Tenants* in Kibana are spaces for saving index patterns, visualizations, dashboards, and other Kibana objects. By default, all Kibana users have access to two tenants: **Private** and **Global**. The global tenant is shared between every Kibana user. The private tenant is exclusive to each user and can't be shared.

Tenants are useful for safely sharing your work with other Kibana users. You can control which roles have access to a tenant and whether those roles have read or write access.

You might use the private tenant for exploratory work, create detailed visualizations with your team in an `analysts` tenant, and maintain a summary dashboard for corporate leadership in an `executive` tenant.

If you share a visualization or dashboard with someone, you can see that the URL includes the tenant:

```
http://<kibana_host>:5601/app/kibana?security_tenant=analysts#/visualize/edit/c501fa50-7e52-11e9-ae4e-b5d69947d32e?_g=()
```


## Configuration

Multi-tenancy is enabled by default, but you can disable it or change its settings using `plugins/opendistro_security/securityconfig/config.yml`:

```yml
config:
  dynamic:
    kibana:
      multitenancy_enabled: true
      server_username: kibanaserver
      index: '.kibana'
    do_not_fail_on_forbidden: false
```

Setting | Description
:--- | :---
`multitenancy_enabled` | Enable or disable multi-tenancy. Default is true.
`server_username` | Must match the name of the Kibana server user from `kibana.yml`. Default is `kibanaserver`.
`index` | Must match the name of the Kibana index from `kibana.yml`. Default is `.kibana`.
`do_not_fail_on_forbidden` | If true, the security plugin removes any content that a user is not allowed to see from search results. If false, the plugin returns a security exception. Default is false.

`kibana.yml` has some additional settings:

```yml
elasticsearch.username: kibanaserver
elasticsearch.password: kibanaserver
elasticsearch.requestHeadersWhitelist: ["securitytenant","Authorization"]
opendistro_security.multitenancy.enabled: true
opendistro_security.multitenancy.tenants.enable_global: true
opendistro_security.multitenancy.tenants.enable_private: true
opendistro_security.multitenancy.tenants.preferred: ["Private", "Global"]
opendistro_security.multitenancy.enable_filter: false
```

Setting | Description
:--- | :---
`elasticsearch.requestHeadersWhitelist` | Kibana requires that you whitelist all HTTP headers that it passes to Elasticsearch. Multi-tenancy uses a specific header, `securitytenant`, that must be present with the standard `Authorization` header. If the `securitytenant` header is not whitelisted, Kibana starts with a red status.
`opendistro_security.multitenancy.enabled` | Enables or disables multi-tenancy in Kibana. Default is true.
`opendistro_security.multitenancy.tenants.enable_global` | Enables or disables the global tenant. Default is true.
`opendistro_security.multitenancy.tenants.enable_private` | Enables or disables the private tenant. Default is true.
`opendistro_security.multitenancy.tenants.preferred` | Lets you change ordering in the **Tenants** tab of Kibana. By default, the list starts with global and private (if enabled) and then proceeds alphabetically. You can add tenants here to move them to the top of the list.
`opendistro_security.multitenancy.enable_filter` | If you have many tenants, you can add a search bar to the top of the list. Default is false.


## Add tenants

To create tenants, use Kibana, the REST API, or `tenants.yml`.


#### Kibana

1. Open Kibana.
1. Choose **Security**, **Tenants**, and **Create tenant**.
1. Give the tenant a name and description.
1. Choose **Create**.


#### REST API

See [Create tenant](../api/#create-tenant).


#### tenants.yml

```yml
---
_meta:
  type: "tenants"
  config_version: 2

## Demo tenants
admin_tenant:
  reserved: false
  description: "Demo tenant for admin user"
```

## Give roles access to tenants

After creating a tenant, give a role access to it using Kibana, the REST API, or `roles.yml`.

- Read-write (`kibana_all_write`) permissions let the role view and modify objects in the tenant.
- Read-only (`kibana_all_read`) permissions let the role view objects, but not modify them.


#### Kibana

1. Open Kibana.
1. Choose **Security**, **Roles**, and a role.
1. For **Tenant permissions**, add tenants, press Enter, and give the role read and/or write permissions to it.


#### REST API

See [Create role](../API/#create-role).


#### roles.yml

```yml
---
test-role:
  reserved: false
  hidden: false
  cluster_permissions:
  - "cluster_composite_ops"
  - "indices_monitor"
  index_permissions:
  - index_patterns:
    - "movies*"
    dls: ""
    fls: []
    masked_fields: []
    allowed_actions:
    - "read"
  tenant_permissions:
  - tenant_patterns:
    - "human_resources"
    allowed_actions:
    - "kibana_all_read"
  static: false
_meta:
  type: "roles"
  config_version: 2
```


## Manage Kibana indices

The open source version of Kibana saves all objects to a single index: `.kibana`. The security plugin uses this index for the global tenant, but separate indices for every other tenant. Each user also has a private tenant, so you might see a large number of indices that follow two patterns:

```
.kibana_<hash>_<tenant_name>
.kibana_<hash>_<username>
```

The security plugin scrubs these index names of special characters, so they might not be a perfect match of tenant names and usernames.
{: .tip }

To back up your Kibana data, [take a snapshot](../../elasticsearch/snapshot-restore/) of all tenant indices using an index pattern such as `.kibana*`.
