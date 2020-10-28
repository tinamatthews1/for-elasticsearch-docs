---
layout: default
title: Index State Management
nav_order: 34
has_children: true
---

# Index State Management
Kibana
{: .label .label-yellow :}

If you analyze time-series data, you likely prioritize new data over old data. You might periodically perform certain operations on older indices, such as reducing replica count or deleting them.

Index State Management (ISM) is a plugin that lets you automate these periodic, administrative operations by triggering them based on changes in the index age, index size, or number of documents. Using the ISM plugin, you can define *policies* that automatically handle index rollovers or deletions to fit your use case.

For example, you can define a policy that moves your index into a `read_only` state after 30 days and then deletes it after a set period of 90 days. You can also set up the policy to send you a notification message when the index is deleted.

You might want to perform an index rollover after a certain amount of time or run a `force_merge` operation on an index during off-peak hours to improve search performance during peak hours.

To use the ISM plugin, your user role needs to be mapped to the `all_access` role that gives you full access to the cluster. To learn more, see [Users and roles](../security/access-control/users-roles/).
{: .note }

## Get started with ISM

To get started, choose **Index Management** in Kibana.

### Step 1: Set up policies

A policy is a set of rules that describes how an index should be managed. For information about creating a policy, see [Policies](policies/).

1. Choose the **Index Policies** tab.
2. Choose **Create policy**.
3. In the **Name policy** section, enter a policy ID.
4. In the **Define policy** section, enter your policy.
5. Choose **Create**.

After you create a policy, your next step is to attach this policy to an index or indices.
You can also include the `policy_id` in an index template so when an index is created that matches the index template pattern, the index will have the policy attached to it:

```json
PUT _index_template/<template_name>
{
  "index_patterns": ["index_name-*"],                 
  "settings": {      
    "opendistro.index_state_management.policy_id": "policy_id"    
  }
}
```

### Step 2: Attach policies to indices

1. Choose **Indices**.
2. Choose the index or indices that you want to attach your policy to.
3. Choose **Apply policy**.
4. From the **Policy ID** menu, choose the policy that you created.
You can see a preview of your policy.
5. If your policy includes a rollover operation, specify a rollover alias.
Make sure that the alias that you enter already exists. For more information about the rollover operation, see [rollover](policies/#rollover).
6. Choose **Apply**.

After you attach a policy to an index, ISM creates a job that runs every 5 minutes by default to perform policy actions, check conditions, and transition the index into different states. To change the default time interval for this job, see [Settings](settings/).

If you want to use an Elasticsearch operation to create an index with a policy already attached to it, see [create index](api/#create-index).

### Step 3: Manage indices

1. Choose **Managed Indices**.
2. To change your policy, see [Change Policy](managedindices#changepolicy).
3. To attach a rollover alias to your index, select your policy and choose **Add rollover alias**.
Make sure that the alias that you enter already exists. For more information about the rollover operation, see [rollover](policies/#rollover).
4. To remove a policy, choose your policy, and then choose **Remove policy**.
5. To retry a policy, choose your policy, and then choose **Retry policy**.

For information about managing your policies, see [Managed Indices](managedindices/).
