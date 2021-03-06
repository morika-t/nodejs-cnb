# Cloud Foundry Node.js Buildpack v2

[![CF Slack](https://www.google.com/s2/favicons?domain=www.slack.com) Join us on Slack](https://cloudfoundry.slack.com/messages/buildpacks/)

A Cloud Foundry [buildpack](http://docs.cloudfoundry.org/buildpacks/) for Node based apps, composed of [Cloud Native Buildpacks](https://buildpacks.io/).

### Buildpack User Documentation

Official buildpack documentation can be found at [node buildpack docs](http://docs.cloudfoundry.org/buildpacks/node/index.html).

### Building the Buildpack for Use in Cloud Foundry

To build this buildpack, run the following commands from the buildpack's directory:

1. Source the .envrc file in the buildpack directory.

   ```bash
   $ source .envrc
   ```
   To simplify the process in the future, install [direnv](https://direnv.net/) which will automatically source .envrc when you change directories.

1. Install Go, if it is not already installed

    ```bash
    $ ./scripts/install_go.sh
    ```

1. Install the packaging tools

    ```bash
    $ ./scripts/install_shim_tools.sh
    ```

1. Build the buildpack, using [cnb2cf](https://github.com/cloudfoundry/cnb2cf#usage)

    ```bash
   $ cnb2cf package -stack <stack> [-cached] [-version <version>] [-cachedir <path to cachedir>]    
    ```

1. Use in Cloud Foundry

   Upload the buildpack to your Cloud Foundry and optionally specify it by name

    ```bash
    $ cf create-buildpack [BUILDPACK_NAME] [BUILDPACK_ZIP_FILE_PATH] 1
    $ cf push my_app [-b BUILDPACK_NAME]
    ```

### Testing

Buildpacks use the [Cutlass](https://github.com/cloudfoundry/libbuildpack/tree/master/cutlass) framework for running integration tests.

To test this buildpack, run the following command from the buildpack's directory:

1. Source the .envrc file in the buildpack directory.

   ```bash
   $ source .envrc
   ```
   To simplify the process in the future, install [direnv](https://direnv.net/) which will automatically source .envrc when you change directories.

1. Install Go, if it is not already installed

    ```bash
    $ ./scripts/install_go.sh
    ```

1. Run integration tests

   Buildpacks use the [Cutlass](https://github.com/cloudfoundry/libbuildpack/tree/master/cutlass) framework for running integration tests against Cloud Foundry. Before running the integration tests, you need to login to your Cloud Foundry using the [cf cli](https://github.com/cloudfoundry/cli):
   
    ```bash
    $ cf login -a https://api.your-cf.com -u name@example.com -p pa55woRD
    ```
    
   Note that your user requires permissions to run `cf create-buildpack` and `cf update-buildpack`. 
   
   To run the integration tests, run the following command from the buildpack's directory:
    
    ```bash
    $ ./scripts/integration.sh
    ```
### Contributing

Find our guidelines [here](./CONTRIBUTING.md).

### Help and Support

Join the #buildpacks channel in our [Slack community](http://slack.cloudfoundry.org/).

### Reporting Issues

[Open an issue](https://github.com/cloudfoundry/nodejs-cnb/issues/new) on this project.

### Active Development

The project backlog is on [Pivotal Tracker](https://www.pivotaltracker.com/projects/1042066).
