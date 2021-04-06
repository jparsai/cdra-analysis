# crda-analysis Python (3.6)  Action

A GitHub Action for using Red Hat CodeReady Dependency Analytics platform to detect vulnerabilities in your Python-3.7 projects.

You can use the Action as follows:

```yaml
name: Example workflow using CRDA
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: setup
        run: |
          mkdir -p site-dir
          pip3 install --target=site-dir -r requirements.txt      
      - name: crda-analysis
        uses: fabric8-analytics/cdra-analysis/python-3.7@main
        with:
          manifest-file-path: requirements.txt
          output-file-path: crda-analysis-report.json
          pkg-installation-directory-path: site-dir
        env:
          CRDA_KEY: ${{ secrets.CRDA_KEY }}
      - name: post-action-setup
        run: |
          printf "Report file data:\n"
          cat crda-analysis-report.json
```
