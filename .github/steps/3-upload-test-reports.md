<!--
  <<< Author notes: Step 3 >>>
  Start this step by acknowledging the previous step.
  Define terms and link to docs.github.com.
-->

## Step 3: Upload test reports

_The workflow has finished running! :sparkles:_

So what do we do when we need the work product of one job in another? We can use the built-in [artifact storage](https://docs.github.com/actions/advanced-guides/storing-workflow-data-as-artifacts) to save artifacts created from one job to be used in another job within the same workflow.

To upload artifacts to the artifact storage, we can use an action built by GitHub: [`actions/upload-artifacts`](https://github.com/actions/upload-artifact).

### :keyboard: Activity: Upload test reports

1. Edit your workflow file.
1. Update the `Run markdown lint` step in your `build` job to use `vfile-reporter-json` and output the results to `remark-lint-report.json`.
1. Add a step to your `build` job that uses the `upload-artifact` action. This step should upload the `remark-lint-report.json` file generated by the updated `Run markdown lint` step.
1. Your new `build` should look like this:

   ```yml
   build:
     runs-on: ubuntu-latest
     steps:
       - uses: actions/checkout@v4

       - name: Run markdown lint
         run: |
           npm install remark-cli remark-preset-lint-consistent vfile-reporter-json
           npx remark . --use remark-preset-lint-consistent --report vfile-reporter-json 2> remark-lint-report.json

       - uses: actions/upload-artifact@v3
         with:
           name: remark-lint-report
           path: remark-lint-report.json
   ```

1. Commit your change to this branch.
1. Wait about 20 seconds then refresh this page (the one you're following instructions from). [GitHub Actions](https://docs.github.com/actions) will automatically update to the next step.

Like the upload action to send artifacts to the storage, you can use the download action to download these previously uploaded artifacts from the `build` job: [`actions/download-artifact`](https://github.com/actions/download-artifact). For brevity, we'll skip that step for this course.