# Easy Plays

The `simple_plays` collection contains some example inventory configurations and simple playbooks that may be run standalone or via Kubernetes.

## Contributing
When making modifications to this collection, make sure to increase the `version` values in `operator-config.yaml` and `galaxy.yml`.

To build run:
```
ansible-galaxy collection build --output-path ../../builds
```

## File
The `file` playbook is a simple example of executing a playbook to create or delete a file.

## Standalone - Running collection via CLI
This collection can be run from a terminal via the `ansible-playbook` CLI by providing the `standalone.yaml` 

- Using the defaults provided in `inventories/standalone.yml`
    ```
    ansible-playbook playbooks/file.yml -i inventories/standalone.yml 
    ```
- Overriding defaults via `--extra-vars`
    ```
    ansible-playbook playbooks/file.yml -i inventories/standalone.yml --extra-vars "filepath=/tmp/overriden-file.tmp"
    ```
- Provisioning
    ```
    ansible-playbook playbooks/file.yml -i inventories/standalone.yml --extra-vars "action=provision"
    ```
- Deprovisioning
    ```
    ansible-playbook playbooks/file.yml -i inventories/standalone.yml --extra-vars "action=deprovision"
    ```

## Kubernetes - Being invoked via Operator
When being executed from Kubernetes, the `running_in_k8s` variable and `k8s_action` variable will be automatically set based on a CR's lifecycle.

- Provisioning (equivalent CLI representation)
    ```
    ansible-playbook playbooks/file.yml -i inventories/k8s.yml --extra-vars "k8s_action=provision"
    ```
- Deprovisioning (equivalent CLI representation)
    ```
    ansible-playbook playbooks/file.yml -i inventories/k8s.yml --extra-vars "k8s_action=deprovision"
    ```