# Molecule {{ cookiecutter.scenario_name }} scenario

> A molecule scenario for testing ansible roles using openstack as a platform provider

## Installing molecule

To install molecule, activate your ansible virtualenv (assuming you already have one) and install it using pip:
```bash
pyenv activate <ansible-venv>
pip install molecule
```

## Folder layout

This directory is a molecule scenario. This means that most files in it follow molecule's requirements:

* `molecule.yml`: configures molecule for this scenario, tells it what is the platform its going to deploy and test, what are the requirements, etc...
* `create.yml`: A playbook used to create the platform the molecule tests will be executed on.
* `converge.yml`: A playbook used to provision the platform, don't hesitate to modify it if you need a specific provisionning workflow.
* `verify.yml`: A playbook used to execute tests on the platform, this is where you'll write your test cases.
* `destroy.yml`: A playbook used to destroy the platform created by the `create.yml` playbook.
* `instances_config.yml.j2`: This is a jinja template file used by the create playbook to respect molecule's API contract (tells it what are the machines and how to contact them).

## How to use

You can use molecule's CLI for multiple purposes:

```bash
molecule create -s {{ cookiecutter.scenario_name }} # create the platform
molecule converge -s {{ cookiecutter.scenario_name }} # provision the platform using the role
molecule verify -s {{ cookiecutter.scenario_name }} # execute test cases on the platform
molecule destroy -s {{ cookiecutter.scenario_name }} # destroy the platform
```

Or do it all at once:
```bash
molecule test -s {{ cookiecutter.scenario_name }} # execute all the above commands in one go
```

## Testing roles with dependencies

If your role has other ansible roles as dependencies. Simply create a `requirements.yml` file in your scenario directory and specify it like the following so in the `molecule.yml` file (molecule will handle dependencies installation process).

```yaml
# molecule.yml
dependency:
  name: galaxy
  options:
    requirements-file: requirements.yml
...
```

```yaml
# requirements.yml
- name: dependency_name
  src: <dependency_url>
  version: <version>
  scm: git # optionnal if using https as src
```

## Having the platform being in a specific state before converging

You can have the platform be in a specific state before launching your converge playbook by creating a `preprare.yml` playbook that will describe the state of the platform before converging. This is usefull when testing complex scenarios with other roles as dependencies.
When creating the platform, molecule will also prepare it, launching the `prepare.yml` playbook. This means you won't need to re-run dependencies on the target platform each time you converge.

## Launching this scenario from local

Launching this scenario from a local machine is totally possible if you have an openstack access and the molecule CLI installed.
First, source your `openrc` configuration file, then run the molecule commands.

Once this is done, you can start using molecule CLI like explained previously.
