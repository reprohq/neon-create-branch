<img src="neon.svg" height="48px" />

# Create a Neon Branch

This GitHub action creates a new Neon branch and endpoint. This action is idempotent; it will only create a branch and/or endpoint if they do not already exist, ideal for use in Pull Request and staging builds.

Learn more about Neon branching here: https://neon.tech/docs/introduction/branching

## Examples

### Basic usage

```
- name: Create Neon database branch
  uses: reprohq/neon-create-branch-action@v1
  with:
    project_id: my-neon-project-id
    branch_name: my-new-database-branch
    api_key: my-neon-api-key
    pg_user: postgres-user
    pg_password: postgres-password
```

### With a specified parent branch

By default, Neon will use the primary/main branch as parent. If you would like to specify a different parent branch, use the `parent_id` input.

```
- name: Create Neon database branch
  uses: reprohq/neon-create-branch-action@v1
  with:
    project_id: my-neon-project-id
    branch_name: my-new-database-branch
    parent_id: my-parent-branch-id
    api_key: my-neon-api-key
    pg_user: postgres-user
    pg_password: postgres-password
```

### Branching from a specific point in time

By default, the branch will be taken from the current state of the parent branch. If you would like to branch at an earlier point in history, you can either specify a Log Sequence Number (LSN) - `parent_lsn` - or timestamp - `parent_timestamp`.

#### Using Log Sequence Number (LSN)

```
- name: Create Neon database branch
  uses: reprohq/neon-create-branch-action@v1
  with:
    project_id: my-neon-project-id
    branch_name: my-new-database-branch
    parent_lsn: 7BAD70
    api_key: my-neon-api-key
    pg_user: postgres-user
    pg_password: postgres-password
```

#### Using timestamp

```
- name: Create Neon database branch
  uses: reprohq/neon-create-branch-action@v1
  with:
    project_id: my-neon-project-id
    branch_name: my-new-database-branch
    parent_timestamp: 2023-01-01T12:00:00Z
    api_key: my-neon-api-key
    pg_user: postgres-user
    pg_password: postgres-password
```


## Outputs

| Name | Description |
| :--- | :--- |
| db_url | The full database URL |
| host | The endpoint hostname |
| branch_id | The ID of the created branch |
