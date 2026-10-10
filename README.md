# Zephyr82 Fhem Collection

This repository contains the `zephyr82.fhem` Ansible Collection. The collection assembles some roles that help with configuring basics of a [FHEM](fhem.de) home automation server: a role for installing, backuping up and restoring a FHEM server and configuring the DbLog config file.

## Using this collection

The collection is not yet published on Ansible automation hub or similar platform. It is at the moment soley published on Github. You can nontheless install the collection using `ansible-galaxy`: 

```bash
ansible-galaxy collection install git+https://github.com/zephyr82/ansible-collection-fhem,main
```

See
[Ansible Using Collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html)
for more details.

## Release notes

See the
[changelog](https://github.com/ansible-collections/zephyr82.fhem/tree/main/CHANGELOG.rst).

## Roadmap

* [ ] rework backup and restore roles so that the backuped up files get stored into a directory for the server where they came from, which is not necessarily the one which is addressed by those roles

## More information

- [this collection's github page](https://github.com/Zephyr82/ansible-collection-fhem)
- [Ansible collection development forum](https://forum.ansible.com/c/project/collection-development/27)
- [Ansible User guide](https://docs.ansible.com/ansible/devel/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/devel/dev_guide/index.html)
- [Ansible Collections Checklist](https://docs.ansible.com/ansible/devel/community/collection_contributors/collection_requirements.html)
- [Ansible Community code of conduct](https://docs.ansible.com/ansible/devel/community/code_of_conduct.html)
- [The Bullhorn (the Ansible Contributor newsletter)](https://docs.ansible.com/ansible/devel/community/communication.html#the-bullhorn)
- [News for Maintainers](https://forum.ansible.com/tag/news-for-maintainers)

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
