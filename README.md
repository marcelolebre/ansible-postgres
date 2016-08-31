# Ansible script for Postgres


This ansible script will provision a given VM with a postgres db listening on all addresses and is booted up automatically at machine start time.

## Steps
### 1) Host configuration
Edit ***hosts*** file and add the ip of the machine to provision.

Example:

```
[target-vm]  
192.168.1.1
```

### 2) Configure user

Edit username on ***install-postgres.yml*** file. Depending on your VM setup you may use different users suchs as: ops, admin, root, etc.

Example:

```
remote_user: root
```

### 3) Execute
```
ansible-playbook install-postgres.yml -i hosts
```

### Results

If things go accordingly you should see something like this:

```
PLAY [Install Postgres] ********************************************************

TASK [install python2] *********************************************************
ok: [192.168.1.1]

TASK [dependencies : Update ubuntu] ********************************************
ok: [192.168.1.1]

TASK [dependencies : Install dependencies] *************************************
ok: [192.168.1.1] => (item=[u'libpq-dev', u'python-psycopg2'])

TASK [install : Install Postgres] **********************************************
ok: [192.168.1.1]

TASK [install : Install Postgres-Contrib] **************************************
ok: [192.168.1.1]

TASK [config : Create Postgres User] *******************************************
changed: [192.168.1.1]

TASK [config : Create Postgres Database] ***************************************
changed: [192.168.1.1]

TASK [config : copy postgresl config file] *************************************
changed: [192.168.1.1]

TASK [config : copy postgresl pg_hba file] *************************************
changed: [192.168.1.1]

TASK [launch : Start PostgreSQL and enable at boot] ****************************
ok: [192.168.1.1]

TASK [launch : Restart Postgresql] *********************************************
changed: [192.168.1.1]

PLAY RECAP *********************************************************************
192.168.1.1             : ok=11   changed=5    unreachable=0    failed=0
```