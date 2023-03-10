# 自动发布mdbook产品

在`Github`中，我们可以使用`action`自动发布我们的`mdbook`文档。只要使用下面的配置就行。
```yaml
name: Use mdbook and github action deploy pages to GitHub Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Install mdbook
        uses: extractions/setup-crate@v1
        with:
          owner: rust-lang
          name: mdbook
      - name: Build with mdbook
        run: mdbook build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: "book"

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```
