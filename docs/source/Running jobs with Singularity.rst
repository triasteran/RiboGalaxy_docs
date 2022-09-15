Running jobs with Singularity
=====

.. _Basic setup:

Basic setup
------------

This setup is needed to run jobs and fetch dependencies using Singularity. A lot of containers that are used in bioinformatics have been produced by the 
BioContainers community and we are going to leverage that. In case if some tool was written using Docker package, singularity is able to handle that too. 

Follow this tutorial: `Galaxy and Singularity <https://training.galaxyproject.org/training-material/topics/admin/tutorials/singularity/tutorial.html>`_

Not all of our RiboGalaxy tools can be run in Singularity containers; some of them rely on conda packages.
In this case, we need to have this file: *templates/galaxy/config/dependency_resolvers_conf.xml* with following content: 

.. code-block:: console

   <dependency_resolvers>
       <tool_shed_packages />
           <galaxy_packages />
               <conda />
           <galaxy_packages versionless="true" />
              <conda versionless="true" />
   </dependency_resolvers>


Don't forget to do SNAPSHOT of VM everytime you introduce a new feature. 

Issues
------------

Issue 1: permissions 

.. code-block:: console

   TASK [Gathering Facts] ***********************************************************************************************************************
   fatal: [ribogalaxy.foundation.cloudcix.com]: FAILED! => {"ansible_facts": {}, "changed": false, "failed_modules": {"ansible.legacy.setup": {"failed": true, "module_stderr": "sudo: a password is required\n", "module_stdout": "", "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error", "rc": 1}}, "msg": "The following modules failed to execute: ansible.legacy.setup\n"}
   
   PLAY RECAP ***********************************************************************************************************************************
   ribogalaxy.foundation.cloudcix.com : ok=0    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
   
Solution: 

.. code-block:: console
  
   $ nano hosts
   $ # add this line to the file (pswd = password for admin user): ansible_sudo_pass=pswd 


