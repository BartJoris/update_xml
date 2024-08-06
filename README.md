# Example playbook to update a SSH config file in an XML format

The `playbook.yml` file contains Ansible tasks that modify the `ssh.xml` file located in the `files/` directory. It performs the following operations:

1. Updates existing XML elements using the `lineinfile` module
2. Adds new XML elements using the `lineinfile` module
3. Inserts a new host block using the `blockinfile` module
4. Adds new XML elements using the `xml` module

**Note:** you can automatically generate a backup of the original file by adding the `--backup` flag to the `lineinfile` and `blockinfile` modules.

## Usage

1. Ensure your XML file is in the `files/` directory and named `ssh.xml`
2. Review and modify the `playbook.yml` file to match your desired changes
3. Run the playbook with the following command:

   ```bash
   ansible-playbook playbook.yml
   ```
4. After running the playbook you can compare the original and updated files to verify the changes.
   ```bash
   diff files/ssh-original.xml files/ssh.xml

    1c1
    < <?xml version="1.0" encoding="UTF-8"?>
    ---
    > <?xml version='1.0' encoding='UTF-8'?>
    6c6,7
    <   </global-settings>
    ---
    >   <new_element>some_value</new_element></global-settings>
    >   <new_element>some_value</new_element>
    12c13
    <     <user>username</user>
    ---
    > <user>admin</user>
    23a25,34
    > # BEGIN ANSIBLE MANAGED BLOCK
    > <host>
    >   <name>example-server2</name>
    >   <hostname>new.example.com</hostname>
    >   <port>2222</port>
    >   <user>newuser</user>
    >   <identity-file>~/.ssh/new_server_rsa</identity-file>
    >   <forward-agent>yes</forward-agent>
    > </host>
    > # END ANSIBLE MANAGED BLOCK
   ```

   ## Additional resources

   - [Ansible Documentation lineinfile](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/lineinfile_module.html)
   - [Ansible Documentation blockinfile](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/blockinfile_module.html)
   - [Ansible Documentation xml](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/xml_module.html)