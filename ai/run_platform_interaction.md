# Run Platform Interaction Analysis

Read and follow:

`ai/platform_interaction_instructions.md`

Apply the instructions to:

`03_platform_interaction.ipynb`

Do not modify:

- `01_overall_ab_test.ipynb`
- `02_platform_diagnostics.ipynb`
- existing JSON outputs
- existing AI reviewer files

Before making changes, briefly explain the planned implementation and confirm:

- the five metric configurations;
- bootstrap unit: `date × publisher_id`;
- one common cluster draw for Mobile and Desktop.

Then update only:

`03_platform_interaction.ipynb`

Run the notebook and verify that the RPM validation result is reproduced approximately.

If the RPM result changes materially, stop and explain why instead of continuing.