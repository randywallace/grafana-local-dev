# Steps to run Grafana Local

1.Have Azure CLI available on PATH and logged in
  a. Note: Running this inside Docker is a bit tricky
2. Run Submodules
  a. `git submodule update --recursive`
3. Add the following to a new line in grafana/go.mod:
  a. `replace github.com/grafana/grafana-azure-sdk-go => ../grafana-azure-sdk-go`
  b. This will allow building Grafana with a local checkout
4. Build Grafana
  a. cd to grafana submodule
  b. `yarn install --immutable`
  c. `go mod tidy` (may not build in next step, if so, probably just run this again)
  d. `make run`
  e. Assuming all successful, will start running Grafana from port 3000, Ctrl+c out.  Otherwise review errors
5. Build Infinity Plugin
  a. update .tool-versions and swap to Node 16
  b. `yarn install --immutable`
  c. `yarn dev`
  d. `go mod tidy`
  e. `mage -v`
6. Symlink the Plugin
  a. from root of repo
  b. `cd plugins`
  c. `ln -s ../grafana-infinity-datasource/dist ./grafana-infinity-datasource`
7. Start 'er up
  a. run start_server script from repo root (`./start_server`)
  b. for local dev, this is fine :)
