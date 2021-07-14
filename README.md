 # Azure Arc Validation Program 

While Azure Arc can be deployed on any K8s clusters, the Arc validation program provides distinct visibility for integrated K8s platforms and promises quality, support and consistency for Azure Arc customers across different hybrid clusters. 

To realize the promise of Arc feature consistency and high quality on partner platforms, we have built the conformance test framework and automation to continuously test and validate the Arc functionality on validated platforms.

Microsoft will take the ownership of providing the conformance tests covering the functionalities of Arc for K8s and Arc enabled Services.

## Asks on Partners for Conformance Testing Integration

It is recommended that our partners integrate the conformance tests into their CI/CD pipelines to run them at the required cadence.

The conformance tests need to be run every time there's an update (major or minor) to the partner infrastructure or to the Azure Arc components.
The updates to the Azure Arc components can be unpacked as follows:
- **Arc for K8s Platform**: The core Arc for K8s platform with functionalities such as onboarding a cluster to Arc, GitOps etc.
- **Arc enabled Data Services**: Provides fully managed PaaS offerings for SQLMI and PostgreSQL. Data services can be deployed with (directly connected mode) or without (indirectly connected mode) the Arc for K8s platform. Details on connectivity modes can be found [here](https://docs.microsoft.com/en-us/azure/azure-arc/data/connectivity).
- **Arc enabled Services**: The Azure services that use Arc for K8s as a substrate to extend their functionalities to clusters on-prem and on other clouds via the [Cluster Extension](https://docs.microsoft.com/en-us/azure/azure-arc/kubernetes/conceptual-extensions) vehicle. Examples include - Azure Monitor, Azure Defender, Arc Data Services (directly connected mode) etc.

### Testing Strategy

There are 3 components to the testing strategy:
- Partner Infrastructure (M)
- Azure Arc Platform (N)
- Arc enabled Services (O)

The testing effort will involve having complete coverage across all 3 of the above components, details for which can be found [here]().

[Need to link to the public doc, don't want to duplicate too much content]: <>

### Testing Strategy for Indirectly Connected Mode of Data Services

[Dhananjay to elaborate on this]: <>

### Partner Responsibility

1. Partners will run the conformance tests according to the above strategy at least 7 days prior to their public/stable release.
2. Partners will be provided access to a storage account on Azure to upload the test results. These results will then be validated by Microsoft. If successful, the partner is conformant with Azure Arc. If not, the error will be triaged by Microsoft to understand where the issue lies. Partners may be contacted to resolve the issue if required. 
3. Partners will create/maintain the test lab for their respective infrastructure.

### Microsoft Responsibility

Microsoft will provide the testing tools and processes for partners to run the tests on their environments.
1. Partners will be provided with the sonobuoy based test suite comprising of plugins for the Azure Arc Platform as well as each of the Arc enabled Services. This test suite will be updated as the Azure Arc components evolve.
2. Storage accounts for each partner will also be provided. Partners will be given credentials (service principals, storage account SAS token) to publish the test results into these accounts.  
3. In case of failures in the conformance tests on partner infrastructure, Microsoft is responsible for the first round of triaging to figure out where the issue lies. If it's something on Microsoft's side, a fix is pushed to the Azure Arc bits. Conversely, if it's something on the partner infrastructure, the onus is on the partner to provide a fix.
4. Microsoft will also integrate the conformance tests in its E2E Arc for K8s testing and validate these tests on partner infrastructure (where possible) for every major/minor version releases of Arc K8s. The partner infrastructure (k8s distribution in this context) will be provisioned on Azure.

[Not sure if we need to mention point 4]: <>

### Failure to Address Issues in Conformance Testing
If Microsoft discovers that the issue in the tests is on the partner's side:
- If it's a new version of the partner's infrastructure, the public documentation will not be updated to add this new version in the validated partners grid.
- If it's a new version of Azure Arc, the public documentation will be updated to call out this limitation that the new version of Azure Arc is not supported on the failed versions of the partner infrastructure.

# Running the Test Suite

Please refer to [this doc](testsuite/running-tests.md) for running the test suite.