# Hacking

## Development How-to Guides


### Run the HyperShift Operator in a local process

1. Ensure the `KUBECONFIG` environment variable points to a management cluster
   with no HyperShift installed yet.

2. Build HyperShift.

        $ make build

3. Install HyperShift in development mode which causes the operator deployment
   to be deployment scaled to zero so that it doesn't conflict with your local
   operator process. 

        $ bin/hypershift install --development

4. Run the HyperShift operator locally.

        $ bin/hypershift-operator run

### Install HyperShift with a custom image

1. Build and push a custom image build to your own repository.

        make IMG=quay.io/my/hypershift:latest docker-build docker-push

2. Install HyperShift using the custom image:

        $ bin/hypershift install --hypershift-image quay.io/my/hypershift:latest

### Run the e2e tests with a compiled binary

1. Install HyperShift.
2. Run the tests.

        $ make e2e
        $ bin/test-e2e -v -args --ginkgo.v --ginkgo.trace \
          --e2e.quick-start.aws-credentials-file /my/aws-credentials \
          --e2e.quick-start.pull-secret-file /my/pull-secret \
          --e2e.quick-start.ssh-key-file /my/public-ssh-key

### Run the e2e tests with the local source tree

1. Install HyperShift.
2. Run the tests.

        $ go test -tags e2e -v ./test/e2e -args --ginkgo.v --ginkgo.trace \
          --e2e.quick-start.aws-credentials-file /my/aws-credentials \
          --e2e.quick-start.pull-secret-file /my/pull-secret \
          --e2e.quick-start.ssh-key-file /my/public-ssh-key

### Visualize the Go dependency tree

MacOS
```
brew install graphviz
go get golang.org/x/exp/cmd/modgraphviz
go mod graph | modgraphviz | dot -T pdf | open -a Preview.app -f
```
