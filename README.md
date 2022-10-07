# ServiceNow ITSM Actions

ServiceNow ITSM Actions powered by Ansible.

 ![](https://github.com/abirismyname/create-discussion/workflows/tests/badge.svg) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

## About

This action provides a wrapper around [Ansible Collection for ServiceNow ITSM](https://galaxy.ansible.com/servicenow/itsm) to perform operations on a ServiceNow instance. The Ansible Collection for ServiceNow IT Service Management (ITSM) includes a variety of Ansible content to help automate the management of ServiceNow IT Service Management.

## Usage

In your workflow, to perform a new operation, include a step like this:

```yaml
      - name: Let it SNOW
        uses: shundor/servicenow-actions@main
        with: 
          sn_host:  "${{ secrets.SN_HOST }}"
          sn_username: "${{ secrets.SN_USERNAME }}"
          sn_password: "${{ secrets.SN_PASSWORD }}"
          sn_client_id: "${{ secrets.SN_CLIENT_ID }}"
          sn_client_secret: "${{ secrets.SN_CLIENT_SECRET }}"
          sn_module: "${{ secrets.SN_MODULE }}"
          sn_module_params: "${{ secrets.SN_MODULE_PARAMS }}"            
```

## Inputs

The following inputs are _required_:

- `sn_host`: The ServiceNow instance hostname
- `sn_username`: The ServiceNow username
- `sn_password`: The ServiceNow password
- `sn_client_id`: The ServiceNow client ID
- `sn_client_secret`: The ServiceNow client secret
- `sn_module`: The Ansible module to use
- `sn_module_params`: The parameters to pass to the Ansible module

Optional:
- `debug`: When set to `true`, the action save the playbook to a workflow artifact

### Obtaining the `sn_client_id` and `sn_client_secret`
You can create `sn_client_id` and `sn_client_secret` via the Application Registry under System OAuth in ServiceNow.  
[![Screenshot](https://developer.servicenow.com/api/x_snc_devblog/v1/vfs/file?p=/post/connections-and-credentials/application-registry-record.png)](https://developer.servicenow.com/blog.do?p=/post/connections-and-credentials/)

### SN_MODULE
The module parameter must one of the following:
|Name|Description|
|:----|:----|
|[servicenow.itsm.api](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.api_module.rst)|Manage ServiceNow POST, PATCH and DELETE requests|
|[servicenow.itsm.api_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.api_info_module.rst)|Manage ServiceNow GET requests|
|[servicenow.itsm.attachment](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.attachment_module.rst)|a module that users can use to download attachment using sys_id|
|[servicenow.itsm.change_request](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.change_request_module.rst)|Manage ServiceNow change requests|
|[servicenow.itsm.change_request_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.change_request_info_module.rst)|List ServiceNow change requests|
|[servicenow.itsm.change_request_task](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.change_request_task_module.rst)|Manage ServiceNow change request tasks|
|[servicenow.itsm.change_request_task_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.change_request_task_info_module.rst)|List ServiceNow change request tasks|
|[servicenow.itsm.configuration_item](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.configuration_item_module.rst)|Manage ServiceNow configuration items|
|[servicenow.itsm.configuration_item_batch](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.configuration_item_batch_module.rst)|Manage ServiceNow configuration items in batch mode|
|[servicenow.itsm.configuration_item_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.configuration_item_info_module.rst)|List ServiceNow configuration item|
|[servicenow.itsm.incident](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.incident_module.rst)|Manage ServiceNow incidents|
|[servicenow.itsm.incident_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.incident_info_module.rst)|List ServiceNow incidents|
|[servicenow.itsm.problem](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.problem_module.rst)|Manage ServiceNow problems|
|[servicenow.itsm.problem_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.problem_info_module.rst)|List ServiceNow problems|
|[servicenow.itsm.problem_task](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.problem_task_module.rst)|Manage ServiceNow problem tasks|
|[servicenow.itsm.problem_task_info](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.problem_task_info_module.rst)|List ServiceNow problem tasks|

### SN_MODULE_PARAMS

### Example: Creating an Incident

To create an incident, you can use the `servicenow.itsm.incident` module. The following example creates an incident with a short description of "Test Incident" and a description of "This is a test incident created by the ServiceNow Actions GitHub Action":

```yaml
      - name: Create An Incident
        uses: shundor/servicenow-actions@main
        with: 
          sn_host:  "${{ secrets.SN_HOST }}"
          sn_username: "${{ secrets.SN_USERNAME }}"
          sn_password: "${{ secrets.SN_PASSWORD }}"
          sn_client_id: "${{ secrets.SN_CLIENT_ID }}"
          sn_client_secret: "${{ secrets.SN_CLIENT_SECRET }}"
          sn_module: "servicenow.itsm.incident"
          sn_module_params: "${{ secrets.SN_MODULE_PARAMS }}"
```

The value for the SN_MODULE_PARAMS secret should be:
```yaml
caller: admin
short_description: Test Incident
description: This is a test incident created by the ServiceNow Actions GitHub Action
impact: low
urgency: low
```

For all the different parameters that can be passed to the `servicenow.itsm.incident` module, see the [docs](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.incident_module.rst) on GitHub.

### Example: Get Info on a specific Incident

To get info on a specific incident, you can use the `servicenow.itsm.incident_info` module. The following example gets details about Incident incident_info:

```yaml
      - name: Retrieve Incident INC0000039
        uses: shundor/servicenow-actions@main
        id: snow
        with: 
          sn_host:  "${{ secrets.SN_HOST }}"
          sn_username: "${{ secrets.SN_USERNAME }}"
          sn_password: "${{ secrets.SN_PASSWORD }}"
          sn_client_id: "${{ secrets.SN_CLIENT_ID }}"
          sn_client_secret: "${{ secrets.SN_CLIENT_SECRET }}"
          sn_module: "servicenow.itsm.incident_info"
          sn_module_params: "${{ secrets.SN_MODULE_PARAMS }}"
      - name: Write to file
        uses: frdrwrt/write-to-file@v1.3
        with:
          filepath: output.json
          mode: 0777
          content: ${{ steps.snow.outputs.output }}
      - name: Display output
        shell: bash
        run: |
            jq '.plays[].tasks[].hosts.localhost.records[]' output.json          
```

The value for the SN_MODULE_PARAMS secret should be:
```yaml
number: INC0000039
```

For all the different parameters that can be passed to the `servicenow.itsm.incident_info_module` module, see the [docs](https://github.com/ansible-collections/servicenow.itsm/blob/main/docs/servicenow.itsm.incident_info_module.rst) on GitHub. The `output` parameter will contain all the information about the incident.
## Outputs

This action provides the following outputs:
- `output`: The captured output as JSON
## Credits

- :bow: Based on [action-ansible-playbook](https://github.com/marketplace/actions/run-ansible-playbook) by [dawidd6](https://github.com/dawidd6)
- :bow: This action relies on [Ansible Collection for ServiceNow ITSM](https://galaxy.ansible.com/servicenow/itsm)
