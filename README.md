# ansible-role-grafana
Ansible role to install Grafana Server.

Grafana is a tool that can Query, visualize, alert on, and understand your data recorded in external database.   Data is visualizsed in flexible dashboards

## Role Variables

### Access settings:

    grafana_admin_password = "SET_ADMIN_PASSWORD_HERE"

Set the password to access to web interface

### Connection settings:

    grafana_listen_port: 3000

Set the tcp port the grafana server will be accessed, default port is 3000. 

### Data sources

    grafana_datasources: 
      - name: prometheus
        type: prometheus
        url: http://127.0.0.1:9090


Set the name of the prometheus datasource that grafana will pull data from

### Dashboard Settings:

    grafana_dashboards:
      - name: Node Exporter
        id: 1860
        rev: 23

Download dashboards from https://grafana.com/grafana/dashboardsdashboards 

## Dependencies

None.

## Example Playbook

    ---
    - name: Install grafana
      hosts: monitor
      become: yes
      roles:
        - grafana
      tags: 
        - grafana

## Reloading / restarting

Key config changes to the config file /etc/grafana/grafana.ini require a full restart

    sudo systemctl restart grafana-server
