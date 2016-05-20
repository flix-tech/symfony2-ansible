# Ansible role to deploy symfony2 projects.

1. Clone project on 127.0.0.1 an run composer install.
2. Deploy project directory to your inventory.
3. Clear cache and make live switch.

This deploy role is using the following directory structure:

```
current -> /var/www/project.tld/releases/2016-01-01-12-12-12
releases
    2016-01-01-12-12-12
    2016-01-02-12-12-12
    ...
shared
    app
        logs
```

Example playbook:

```
-
  hosts: all

  roles:
    - flix-tech.symfony2

  pre_tasks: 

  vars:
    symfony_project_env: prod
    symfony_project_name: project.tld
    symfony_project_repo: git@....git
    symfony_project_web_dir: /var/www/project.tld
    symfony_project_run_migrations: false
    symfony_assetic_dump: true
`
    # Hooks
    symfony_post_install_hook: "{{ playbook_dir }}/files/hooks/post_install.yml"
    symfony_post_finish_hook: "{{ playbook_dir }}/files/hooks/post_finish.yml"

  environment:
    SYMFONY_ENV: "{{ symfony_project_env }}"
``
