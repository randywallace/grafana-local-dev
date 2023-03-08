# Steps to run Grafana Local


1. Have Azure CLI available on PATH and logged in
  - Note: Running this inside Docker is a bit tricky
1. Run Submodules
  - `git submodule update --recursive`
1. Add the following to a new line in grafana/go.mod:
  - `replace github.com/grafana/grafana-azure-sdk-go => ../grafana-azure-sdk-go`
  - This will allow building Grafana with a local checkout
1. Build Grafana
  - cd to grafana submodule
  - `yarn install --immutable`
  - `go mod tidy` (may not build in next step, if so, probably just run this again)
  - `make run`
  - Assuming all successful, will start running Grafana from port 3000, Ctrl+c out.  Otherwise review errors
1. Build Infinity Plugin
  - update .tool-versions and swap to Node 16
  - `yarn install --immutable`
  - `yarn dev`
  - `go mod tidy`
  - `mage -v`
1. Symlink the Plugin
  - from root of repo
  - `cd plugins`
  - `ln -s ../grafana-infinity-datasource/dist ./grafana-infinity-datasource`
1. Start 'er up
  - run start_server script from repo root (`./start_server`)
  - for local dev, this is fine :)
