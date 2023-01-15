# Configuration

::: molecule.config.Config

## Prerun

In order to help Ansible find used modules and roles, molecule will
perform a prerun set of actions. These involve installing dependencies
from `requirements.yml` specified at project level, install a standalone
role or a collection. The destination is `project_dir/.cache` and the
code itself was reused from ansible-lint, which has to do the same
actions. (Note: ansible-lint is not included with molecule.)

This assures that when you include a role inside molecule playbooks,
Ansible will be able to find that role, and that the include is exactly
the same as the one you are expecting to use in production.

If for some reason the prerun action does not suits your needs, you can
still disable it by adding `prerun: false` inside the
configuration file.

Keep in mind that you can add this value to the
`.config/molecule/config.yml` file, in your `$HOME` or at the root of
your project, in order to avoid adding it to each scenario.

## Role name check

By default, `Molecule` will check whether the role name follows the name
standard. If not, it will raise an error.

If computed fully qualified role name does not follow current galaxy
requirements, you can ignore it by adding [role_name_check:
1]{.title-ref} inside the configuration file.

It is strongly recommended to follow the name standard of
[namespace](https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations)
and
[role](https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names).

## Variable Substitution

::: molecule.interpolation.Interpolator

There are following environment variables available in `molecule.yml`:

MOLECULE_DEBUG

: If debug is turned on or off

MOLECULE_FILE

: Path to molecule config file, usually
`~/.cache/molecule/<role-name>/<scenario-name>/molecule.yml`

MOLECULE_ENV_FILE

: Path to molecule environment file, usually `<role_path>/.env.yml`

MOLECULE_STATE_FILE

: Path to molecule state file, contains state of the instances
(created, converged, etc.). Usually
`~/.cache/molecule/<role-name>/<scenario-name>/state.yml`

MOLECULE_INVENTORY_FILE

: Path to generated inventory file, usually
`~/.cache/molecule/<role-name>/<scenario-name>/inventory/ansible_inventory.yml`

MOLECULE_EPHEMERAL_DIRECTORY

: Path to generated directory, usually
`~/.cache/molecule/<role-name>/<scenario-name>`

MOLECULE_SCENARIO_DIRECTORY

: Path to scenario directory, usually
`<role_path>/molecule/<scenario-name>`

MOLECULE_PROJECT_DIRECTORY

: Path to your project (role) directory, usually `<role_path>`

MOLECULE_INSTANCE_CONFIG

: Path to the instance config file, contains instance name,
connection, user, port, etc. (populated from driver). Usually
`~/.cache/molecule/<role-name>/<scenario-name>/instance_config.yml`

MOLECULE_DEPENDENCY_NAME

: Dependency type name, usually 'galaxy'

MOLECULE_DRIVER_NAME

: Name of the molecule scenario driver

MOLECULE_PROVISIONER_NAME

: Name of the provisioner tool (usually 'ansible')

MOLECULE_REPORT

: Name of HTML file where to dump execution report.

MOLECULE_SCENARIO_NAME

: Name of the scenario

MOLECULE_VERBOSITY

: Determine Ansible verbosity level.

MOLECULE_VERIFIER_NAME

: Name of the verifier tool (usually 'ansible')

MOLECULE_VERIFIER_TEST_DIRECTORY

: Path of the directory that contains verifier tests, usually
`<role_path>/<scenario-name>/<verifier-name>`

# Dependency

Testing roles may rely upon additional dependencies. Molecule handles
managing these dependencies by invoking configurable dependency
managers.

## Ansible Galaxy

::: molecule.dependency.ansible_galaxy.AnsibleGalaxy

## Shell

::: molecule.dependency.shell.Shell

# Driver

Molecule uses [Ansible](#ansible-1) to manage instances to operate on.
Molecule supports any provider [Ansible](#ansible-1) supports. This work
is offloaded to the [provisioner]{.title-ref}.

The driver's name is specified in [molecule.yml]{.title-ref}, and can
be overridden on the command line. Molecule will remember the last
successful driver used, and continue to use the driver for all
subsequent subcommands, or until the instances are destroyed by
Molecule.

!!! warning

    The verifier must support the Ansible provider for proper Molecule
    integration.

    The driver's python package requires installation.

## Delegated

::: molecule.driver.delegated.Delegated

# Platforms

::: molecule.platforms.Platforms

# Provisioner

Molecule handles provisioning and converging the role.

## Ansible

::: molecule.provisioner.ansible.Ansible

# Scenario {#root_scenario}

Molecule treats scenarios as a first-class citizens, with a top-level
configuration syntax.

::: molecule.scenario.Scenario

# State

An internal bookkeeping mechanism.

::: molecule.state.State

# Verifier

Molecule handles role testing by invoking configurable verifiers.

## Ansible

::: molecule.verifier.ansible.Ansible

## Testinfra

::: molecule.verifier.testinfra.Testinfra
