systemd_service
=========

This role is used to create systemd services on the target server using binaries
already on the server or uploaded binaries, it also sets up syslog so each service's
output is redirected to a different file.


Role Variables
--------------

This role requires only one variable called `systemd_services` which is an array of
dictionaries and each dictionary has the following options:

* name: The name of the service (required)
* src: The location of program to be uploaded on ansible control machine. (optional)
* dst: The location of the program on the server where it will be uploaded. (required)
* upload: A boolean option that tells if the program must be uploaded or not. (optional defaults to False)
* type: This tells the service's type (simple, forking). (optional defaults to simple)
* pid_file: This tells the location of the file where the PID of the child process
is stored in case of forking service. (required when type == "forking")
* description: This is the description of the service. (optional)
* log_file: This specifies the location of the file used to send logs to it. (optional)
* started: This boolean tells whether the service must be started or not. (optional defaults to False)

Example Playbook
----------------

    - hosts: server1
      vars:
        - systemd_service:
          - src: test
            dst: /usr/local/bin/test
            name: test
            upload: True
            type: simple
            log_file: /var/log/test.log
            started: True
          - dst: /us/local/bin/dst
            description: a forking service test
            started: True
            type: forking
            pid_file: /var/run/dst.log
      roles:
         - { role: mohsensy.systemd_service }

License
-------

BSD

Author Information
------------------

If you have any questions or suggestions please contact me on

[twitter](https://twitter.com/mouhsen_ibrahim)

[linkedin](https://linkedin.com/in/mohsen-ibrahim-670b13112/)

[email](mailto:mohsen47@hotmail.co.uk)
