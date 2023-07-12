# ansible-role-grafana
![CI](https://github.com/miarec/ansible-role-grafana/actions/workflows/ci.yml/badge.svg?event=push)

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
        dashboard_id: 1860
        revision_id: 23
        datasource: prometheus
        default: true
      - name: Process Exporter
        dashboard_id: 249
        revision_id: 2
        datasource: prometheus
        default: false

Download dashboards from https://grafana.com/grafana/dashboards

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

# ToDo
 - dashboards are not removed if not on list
 - add unit testing