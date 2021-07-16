 # Azure Arc Validation Program 

While Azure Arc can be deployed on any K8s clusters, the Arc validation program provides distinct visibility for integrated K8s platforms and promises quality, support and consistency for Azure Arc customers across different hybrid clusters. 

To realize the promise of Arc feature consistency and high quality on partner platforms, we have built the conformance test framework and automation to continuously test and validate the Arc functionality on validated platforms.

Microsoft will take the ownership of providing the conformance tests covering the functionalities of Arc for K8s and Arc enabled Data Services.

## Asks on Partners for Conformance Testing Integration

It is recommended that our partners integrate the conformance tests into their CI/CD pipelines to run them at the required cadence.

The conformance tests need to be run every time there's an update (major or minor) to the partner offering or to the Azure Arc components.
These components include*:
- **Arc for K8s Platform**: The core Arc for K8s platform with functionalities such as onboarding a cluster to Arc, GitOps etc.
- **Arc enabled Data Services**: Provides fully managed Azure PaaS offerings for SQLMI and PostgreSQL on your clusters on-prem or on other clouds.

*These components may grow in the future as the Azure Arc portfolio widens.

### Testing Strategy

The testing strategy can be broken down into two parts:
- **Update to partner offering**: The new version of the partner offering is tested against N, N-1 and N-2 minor versions of Arc for K8s and Arc enabled Data Services.
- **Update to Azure Arc components**: The new version of the Azure Arc component is tested against N, N-2 and N-2 minor versions of the partner offering.

| Arc for K8s Minor Release | Version |
| :---: | :----: |
| N | 1.3.8 |
| N-1 | 1.2.0 |
| N-2 | 1.1.0 |

### Partner Responsibility

1. Partners will run the conformance tests according to the above strategy and produce successful results at least 7 days prior to their public/stable release.
2. Partners will be provided access to a storage account on Azure to upload the test results. These results will then be validated by Microsoft. If successful, the partner is conformant with Azure Arc. If not, the error will be triaged by Microsoft to understand where the issue lies. Partners may be contacted to resolve the issue if required. 
3. Partners will create/maintain the test lab for their respective offering.

### Microsoft Responsibility

Microsoft will provide the testing tools and processes for partners to run the tests on their environments.
1. Microsoft will update partners on the availability of a new version of an Azure Arc component at least 30 days prior to the release.
2. Partners will be provided with the sonobuoy based test suite comprising of plugins for the Arc for K8s as well as Arc enabled Data Services. This test suite will be updated as the Azure Arc components evolve.
3. Storage accounts for each partner will also be provided. Partners will be given credentials (service principals, storage account SAS token) to publish the test results into these accounts.  
4. In case of failures in the conformance tests on partner offering, Microsoft will do the first round of triaging to figure out where the issue lies. If it's something on Microsoft's side, a fix is pushed to the Azure Arc components. Conversely, if it's something on the partner offering, the onus is on the partner to provide a fix.

### Failure to Address Issues in Conformance Testing
If Microsoft discovers that the issue in the tests is on the partner's side:
- If it's a new version of the partner's offering, the public documentation will not be updated to add this new version in the validated partners grid unless the issue is fixed.
- If it's a new version of Azure Arc, the public documentation will be updated to call out this limitation that the new version of Azure Arc is not supported on the failed versions of the partner offering.

# Running the Test Suite

Please refer to [this doc](testsuite/running-tests.md) for running the test suite.