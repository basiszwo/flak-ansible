# Role: deploy-user

This role creates a ssh user `deploy` which is being used for (mainly) deploying a ruby on rails
application. It basically can be used for any kind of application deployments.

The name of the deployment user can be changed in each playbook by defining a `deploy_user` variable.

## SSH access

In most cases there are a couple of users who are able to deploy the application.
Within the playbook definition you define a list of users with the `ssh_users` variable.

```
ssh_users:
  - sb
  - foo/bar
```

By convention the **public** ssh keys (from the example) are expected at `files/sb.pub` and `files/foo/bar.pub`.
