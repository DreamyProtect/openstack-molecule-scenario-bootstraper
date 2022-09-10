# openstack-molecule-scenario-bootstraper

> A project using cookiecutter to bootstrap an ansible molecule scenario using Openstack for ansible roles testing

## Usage

To use this project, you must first install cookiecutter:

```bash
pip install cookiecutter
```

Once you've installed cookiecutter, you can create and go in the molecule directory of the ansible role you want to add and generate the scenario:

```bash
cd <role_project>
mkdir molecule && cd molecule
cookiecutter git@github.com:DreamyProtect/openstack-molecule-scenario-bootstraper.git
```

Answer the questions asked by cookiecutter and voila ! The project should've created a molecule scenario after the name you've given it in the molecule folder that you can launch using :

```bash
molecule test -s <my-scenario-name>
```

## Customizing

If you need to add specific security group rules for the instances, you can do so by adding them in the `create.yml` and `destroy.yml` files.

## Contributing

Feel free to submit a PR or an issue if you feel like a feature should be implemented in this project.

To create your development environment you can create a python virtualenv and use the requirements.txt to install all the dependencies required.
