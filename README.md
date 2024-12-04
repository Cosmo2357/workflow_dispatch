
# Manual Trigger (workflow_dispatch)

The workflow_dispatch feature allows you to trigger a workflow manually. You can navigate to the "Actions" tab in your GitHub repository and click on the "Run workflow" button to start the workflow. This capability makes it easier to execute jobs whenever necessary, rather than relying solely on automatic triggers like push or pull_request.

GUI Elements in the Workflow

Dropdown Menu: This workflow includes a dropdown menu for selecting the deployment environment. Available options are development, staging, and production. The default value is set to development.

Checkbox (Boolean): You can use a checkbox to enable or disable a feature flag (Enable new feature?). The default setting is false.

Text Input: Additional tests can be specified through a simple text input field. You can list the tests that should be executed, such as test1, test2, etc.

YAML Code Example

Here is the YAML code that configures the manual trigger with dropdowns, checkboxes, and text inputs:
```yaml
yaml
name: Manual Trigger with Dropdown and Checklist

on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Select the deployment environment'
        required: true
        type: choice
        options:
          - development
          - staging
          - production
        default: development

      feature_flag:
        description: 'Enable new feature?'
        required: true
        type: boolean
        default: false

      additional_tests:
        description: 'Select additional tests to run (check all that apply)'
        required: false
        default: 'test1, test2'

jobs:
  demo_job:
    runs-on: ubuntu-latest

    steps:
      - name: Check out the repository
        uses: actions/checkout@v3

      - name: Display Inputs
        run: |
          echo "Environment selected: ${{ github.event.inputs.environment }}"
          echo "Feature flag enabled: ${{ github.event.inputs.feature_flag }}"
          echo "Additional tests: ${{ github.event.inputs.additional_tests }}"
```

How to Use

Navigate to the "Actions" tab in your repository.

Select the workflow from the list.

Click the "Run workflow" button and fill out the available fields.

Choose the environment from the dropdown list.

Check the box to enable or disable the feature flag.

Optionally input additional tests.

This workflow offers flexibility in triggering different environments or features without altering the YAML file directly.
