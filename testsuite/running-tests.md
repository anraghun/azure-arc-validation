# Running the Conformance Test Suite

This document will enumerate everything you need to do run the sonobuoy based conformance test suite on your environment.

## Running the Arc for K8s and Arc Enabled Services tests

### Prerequisites

1. Set the `KUBECONFIG` environment variable to the path to your kubeconfig file of your cluster.
2. Install [sonobuoy](https://github.com/vmware-tanzu/sonobuoy#installation). Run `sonobuoy version` to verify it's installed correctly.
3. Address the [network requirements](https://docs.microsoft.com/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster#meet-network-requirements) on your cluster for the Arc agents to communicate with Azure.
4. Download and install [git](https://git-scm.com/downloads).
5. Download and install [az cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

### Running the script and publishing the results

1. Clone this repository.
2. Edit the [`partner-metadata.md`](partner-metadata.md) file and fill in the required details.
3. Edit the [`conformance-test-suite.sh`](conformance-test-suite.sh) file and set the values for the required environment variables. Also opt-in to additional functionalities in the test library by un-commenting the code based on if that scenario fits your requirements.
4. Make the test suite file executable by running `chmod +x conformance-test-suite.sh`.
5. Execute the script by running `./conformance-test-suite.sh`.
6. The test suite will take the storage account details as environment variables and will handle publishing the results in the right format.
7. The test catalog can be found [here](catalog.md).

### Retrieving the results

1. Once the above script executes successfully, you can run `sonobuoy retrieve` to get the tar file with the test results and logs.
2. Run `sonobuoy results <path_to_tar>` to display the results. The results are displayed per sonobuoy plugin.
3. To take a deeper look at the test logs:
    1. Extract the tar file by running `tar -xvzf <path_to_tar>`
    2. You will find the pod logs in the `podlogs` folder and the test logs for each test per plugin in the `plugins` folder.

### Cleaning up the test cluster

Sonobuoy creates a few resources (a namespace and some cluster scoped resources) which remain in the cluster unless explicitly cleaned.

Run `sonobuoy delete --wait` to cleanup all sonobuoy resources. This step is important as failing to do so will prevent you from running sonobuoy tests again on the cluster.

## Running the Data Services (Indirectly Connected Mode) tests

### Prerequisites

1. All prerequisites as above
2. [Dhananjay to add other pre-reqs]: <>