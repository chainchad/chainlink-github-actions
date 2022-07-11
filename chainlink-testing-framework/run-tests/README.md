## Docs for the Action
### This action runs chainlink-testing-framework based tests. These can be integration, chaos, smoke and probably others
### Requires you to have a .tool-versions file with a golang and ginkgo vesrsion defined

### Inputs

### `test_command_to_run`

**Required**The command to run the tests

### `test_download_vendor_packages_command`

The command to download the go modules

### `test_download_ginkgo_command`

The command to download Ginkgo

### `cl_repo`

The chainlik ecr repository to use

### `cl_image_tag`

The chainlink image to use

### `build_guantlet_command`

How to build gauntlet if necessary

### `download_contract_artifacts_path`

Path where the contract artifacts need to be placed

### `publish_report_paths`

The path of the output report

### `publish_check_name`

The check name for publishing the reports

### `CGO_ENABLED`

Whether to have cgo enabled

### `token`

**Required** The github token for github repo priveledges

### `artifacts_location`

Location of where error logs are written

### `QA_AWS_REGION`

**Required** The AWS region to use

### `QA_AWS_ROLE_TO_ASSUME`

**Required** The AWS role to assume

### `QA_KUBECONFIG`

**Required** The kubernetes configuration to use

### Example usage

    uses: smartcontractkit/chainlink-github-actions/chainlink-testing-framework/run-tests@v2.0.0
    with:
        test_command_to_run: make test smoke
        test_download_vendor_packages_command: make download
        test_download_ginkgo_command: make install
        cl_repo: ${{ secrets.QA_AWS_ACCOUNT_NUMBER }}.dkr.ecr.${{ secrets.AWS_REGION }}.amazonaws.com/chainlink
        cl_image_tag: custom.${{ github.sha }}
        build_guantlet_command: make build_gauntlet
        download_artifacts_path: contracts/target/deploy
        publish_report_paths: "./tests-smoke-report.xml"
        publish_check_name: Smoke Test Results
        token: ${{ secrets.GITHUB_TOKEN }}
        CGO_ENABLED: 0
        QA_AWS_REGION: ${{ secrets.AWS_REGION }}
        QA_AWS_ROLE_TO_ASSUME: ${{ secrets.AWS_ROLE_TO_ASSUME }}
        QA_KUBECONFIG: ${{ secrets.KUBECONFIG }}