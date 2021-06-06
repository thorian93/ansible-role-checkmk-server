# Ansible Role: Checkmk Server

 This role sets up the Checkmk Server on Debian/Ubuntu, RHEL/CentOS and Fedora servers. 

[![Ansible Role: Webserver](https://img.shields.io/ansible/role/55242?style=flat-square)](https://galaxy.ansible.com/thorian93/checkmk_server)
[![Ansible Role: Webserver](https:/client/img.shields.io/ansible/quality/55242?style=flat-square)](https://galaxy.ansible.com/thorian93/checkmk_server)
[![Ansible Role: Webserver](https://img.shields.io/ansible/role/d/55242?style=flat-square)](https://galaxy.ansible.com/thorian93/checkmk_server)

## Here be Dragons!

Actually no dragons here (yet).

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: thorian93.checkmk_server
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `vars/Debian.yml` and `vars/RedHat.yml`):

    checkmk_edition: raw

The edition to install.

    checkmk_version: 2.0.0p5
    
The version to install.

    checkmk_verify_setup: 'false'

Whether to verify the downloaded setup file using GPG.

    checkmk_external_url: "{{ inventory_hostname }}"

The external URL of the monitoring server. This is the URL the role [thorian93.checkmk_client](https://galaxy.ansible.com/thorian93/checkmk_client) connects to.

    checkmk_redirect_http_to_https: 'true'

Whether to redirect HTTP access to HTTPS.

    checkmk_create_self_signed_cert: 'true'

Whether to create a self signed certificate or not.

    checkmk_self_signed_cert_subj: "/C=DE/ST=NRW/L=Cologne/O=Org/CN={{ checkmk_external_url }}"
    checkmk_self_signed_certificate_key: "/etc/{{ apache2_http_name }}/ssl/checkmk.key"
    checkmk_self_signed_certificate: "/etc/{{ apache2_http_name }}/ssl/checkmk.crt"

Detailed configuration of the self signed certificate.

    checkmk_custom_cert: 'false'

Whether to use a custom certificate like from a PKI or not.

    checkmk_custom_cert_file: /etc/{{ apache2_http_name }}/ssl/checkmk.crt
    checkmk_custom_cert_key: /etc/{{ apache2_http_name }}/ssl/checkmk.key

Detailed configuration of the custom certificate.

    checkmk_certificate_key: "{{ certbot_cert_path }}/privkey.pem"
    checkmk_certificate: "{{ certbot_cert_path }}/cert.pem"
    checkmk_certificate_chain: "{{ certbot_cert_path }}/fullchain.pem"

These variables configure paths for certificates issued through certbot.

    checkmk_sites:
      - name: main
        state: started
        admin_pw: cmkadmin

A list of sites and their respective states and admin password.

## Dependencies

  - [thorian93.apache2](https://galaxy.ansible.com/thorian93/apache2)

## OS Compatibility

This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    role_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run role."
      hosts: all
      become: yes
      roles:
        - thorian93.checkmk_server

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2021 by [Thorian93](http://thorian93.de/).
