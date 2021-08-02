# ansible-role-grafana
Ansible role to install Grafana Server.

Grafana is a tool that can Query, visualize, alert on, and understand your data recorded in external database.   Data is visualizsed in flexible dashboards

## Role Variables

### Connection settings:

    grafana_listen_port: "3000"

Set the tcp port the grafana server will be accessed, default port is 3000. 

### Users

    grafana_admin_password: "miarec_grafana"

admin password that will be used to administer the system


### Data source

    grafana_datasource_name: "prometheus"


Set the name of the prometheus datasource that grafana will pull data from


### Dashboard Settings:

    grafana_dash_id: "1860"
    grafana_dash_rev: "23"

Choose the default Dashboard that will be displayed when logging into the grafana instanace, https://grafana.com/grafana/dashboardsdashboards 

## Dependencies

None.

## Example Playbook

    ---
    - name: Install grafana
      hosts: monitor
      become: yes
      pre_tasks:
        - include_vars: vars/custom.yml
          failed_when: false
      roles:
        - role: 'grafana'
          tags: 'grafana'

## Reloading / restarting

Key config changes to the config file /etc/grafana/grafana.ini require a full restart

    sudo systemctl restart grafana-server
