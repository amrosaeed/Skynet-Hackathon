
Open DEFI Hackathon - Skynet challenge
### Adding Skynet Action to Workflow

Please create a file in your code source “.github/workflows/deploy.yml” with the most basic workflow and add the following:

```
      - name: Deploy to Skynet
        uses: SkynetLabs/deploy-to-skynet-action@v2
        with:
          upload-dir: public
          github-token: ${{ secrets.GITHUB_TOKEN }}
          registry-seed: ${{ secrets.REGISTRY_SEED || '' }}
          registry-datakey: ${{ secrets.REGISTRY_DATAKEY || '' }}
```

source: https://docs.siasky.net/developer-guides/deploy-github-actions

### For project's full .yml file

```
name: Deploy to Skynet

on:
  pull_request:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: "16"

      - run: npm install
      - run: npm run build
      - name: "Deploy to Skynet"
        uses: skynetlabs/deploy-to-skynet-action@v2
        with:
          upload-dir: build
          github-token: ${{ secrets.GITHUB_TOKEN }}
          registry-seed: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' && secrets.REGISTRY_SEED || '' }}
```
