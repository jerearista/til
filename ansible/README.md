# Ansible stuff

- Human formatted debug info:
   ```
   shell ANSIBLE_STDOUT_CALLBACK=debug \
   ansible-playbook -i inventory generate_configs.yml
   ```
- http://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html
- http://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html
-[Specify different hosts in a single playbook file](https://serverfault.com/questions/767716/how-to-specify-different-hosts-for-different-playbooks-in-one-ansible-script)
- [AWX with Docker](https://www.jeffgeerling.com/blog/2017/get-started-using-ansible-awx-open-source-tower-version-one-minute)
- [Managing 15,000 network devices with Ansible](https://www.youtube.com/watch?v=HtMeDbGEylU&feature=youtu.be)
- Include_vars
   ```
   tasks:
     - name: "INCLUDE SOME OTHER VARS"
       include_vars:
         file: "othervars.yml"
   ```
- [Data filters](http://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html#set-theory-filters)
        msg: "{{ show_vlan_after.stdout.0 }}"
- [Dump all vars](https://coderwall.com/p/13lh6w/dump-all-variables)
   ```
    - name: Copy ALL vars to file
      copy:
        content: |
          Module Variables ("vars"):
          --------------------------------
          {{ vars | to_nice_json }} 

          Environment Variables ("environment"):
          --------------------------------
          {{ environment | to_nice_json }} 

          GROUP NAMES Variables ("group_names"):
          --------------------------------
          {{ group_names | to_nice_json }}

          GROUPS Variables ("groups"):
          --------------------------------
          {{ groups | to_nice_json }}

          HOST Variables ("hostvars"):
          --------------------------------
          {{ hostvars | to_nice_json }} 
        dest: /tmp/ansible_vars
   ```

## Extra-vars

```
ansible-playbook -vvv vlan_management.yml \
    --extra-vars='{"ticket_number": "CHG0030079", "vlan_data": { "device": "nyc-sw-02", "id": 982, "name": "TEST_82"}}'
```

As of Ansible 1.3, extra vars can be formatted as YAML, either on the command line or in a file. See the Ansible documentation titled Passing Variables On The Command Line.

```
--extra-vars "@some_file.json"
```

## Inventory

- `ansible-inventory -i inventory --list` NOTE: group_vars will be replicated to each host entry (https://github.com/ansible/ansible/issues/30877)
- Example INI style
   ```
   [atlanta]
   host1
   host2

   [raleigh]
   host2
   host3

   [southeast:children]
   atlanta
   raleigh

   [southeast:vars]
   some_server=foo.southeast.example.com
   halon_system_timeout=30
   self_destruct_countdown=60
   escape_pods=2

   [usa:children]
   southeast
   northeast
   southwest
   northwest
   ```

# AWX

- See inventory being passed to playbooks: ` /api/v2/inventories/N/script/?hostvars=1`
- AWX vars in playbooks:
   ```
   "awx_job_id": 443, 
   "awx_job_launch_type": "scheduled", 
   "awx_job_template_id": 27, 
   "awx_job_template_name": "ServiceNow VLAN Management", 
   "awx_project_revision": "c8269daabcf63e1645e114ffb72cdad0e40ff4f8", 
   "awx_schedule_id": 51, 
   "awx_schedule_name": "VLAN Management: Update ServiceNow Ticket CHG0030122", 
   ```
