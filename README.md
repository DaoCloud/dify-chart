# Dify Helm Chart

This is a Helm Chart for deploying [Dify](https://dify.ai/), an open-source LLMOps platform.

## Installation

### Option 1: Install from Helm Repository (Recommended)

```bash
# Add the Helm repository
helm repo add dify-chart https://daocloud.github.io/dify-chart
helm repo update

# Install the chart
helm install dify dify-chart/dify-chart

# Install with custom namespace
helm install dify dify-chart/dify-chart --namespace dify --create-namespace
```

### Option 2: Install from Local Directory

```bash
# Clone the repository
git clone https://github.com/DaoCloud/dify-chart.git
cd dify-chart

# Install the chart
helm install dify ./dify-chart

# Install with custom namespace
helm install dify ./dify-chart --namespace dify --create-namespace
```

## Configuration

For detailed configuration options, please refer to the [chart documentation](./dify-chart/README.md).

## Releasing New Versions

This project uses GitHub Actions to automate the release process. When a new tag (format: `v*`, e.g. `v0.1.0`) is pushed, it will automatically build and publish the Helm Chart to GitHub Pages.

### Release a New Version

```bash
# Update the version in dify-chart/Chart.yaml
git add dify-chart/Chart.yaml
git commit -m "Bump version to x.y.z"
git tag -a vx.y.z -m "Release version x.y.z"
git push origin main --tags
```

## License

This chart is licensed under the same terms as Dify itself. See the [Dify license](https://github.com/langgenius/dify/blob/main/LICENSE) for details. 