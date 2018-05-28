# ANSIBLE AWS Launch Configuration Role

This is an Ansible role for generating CloudFormation templates and deploying CloudFormation stacks to Amazon Web Services.

## Requirements

- Python 2.7
- PIP package manager (**easy_install pip**)
- Ansible 2.4 or greater (**pip install ansible**)
- Boto3 (**pip install boto3**)
- Netaddr (**pip install netaddr**)
- AWS CLI (**pip install awscli**) installed and configured

## Setup (Pending)

The variables are loaded from group_vars folder. Further customization can be achieved by adding custom var in `all` & respective `roles` folder, under the folder name `vars`.

### Installation using Ansible Galaxy (Pending)

To set this role up as an Ansible Galaxy requirement, first create a `requirements.yml` file in a `roles` subfolder of your playbook and add an entry for this role.  See the [Ansible Galaxy documentation](http://docs.ansible.com/ansible/galaxy.html#installing-multiple-roles-from-a-file) for more details.

```
# Example requirements.yml file
- src: <to be updated>
  scm: git
  version: v1.0
  name: aws-asg-launchConfig
```

Once you have created `requirements.yml`, you can install the role using the `ansible-galaxy` command line tool.

```
$ ansible-galaxy install -r roles/requirements.yml -p ./roles/ --force
```

To update the role version, simply update the `requirements.yml` file and re-install the role as demonstrated above.

### Run Instruction

The following command when run from root of the folder will just gather facts on all the scopes

`ansible-playbook site.yml -e 'debug=true' -e env=asg1 --tags gatherfact -vvv`

Following tags are supported

    - create (For creating LC config)
    - delete (You guessed it!)
    - More coming your way!

The following command is used to create launchConfig, specifically using tags to skip certain playbook. The command will skip deleting launchConfig

`ansible-playbook site.yml -e 'debug=true' -e env=asg1 --skip-tags delete -vvv`

The playbook logic customization/split is done via block in respective `main.yml` for each of the roles

### Invoking STS Role

The following is an example of a playbook configured to use this role.  Note the use of the [AWS STS role](https://github.com/calshankar/Ansible-aws-sts-role.git) to obtain STS credentials is separate from this role.