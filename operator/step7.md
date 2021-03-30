Download and install operator-sdk
Set platform information:
```
export ARCH=$(case $(arch) in x86_64) echo -n amd64 ;; aarch64) echo -n arm64 ;; *) echo -n $(arch) ;; esac)
export OS=$(uname | awk '{print tolower($0)}')
```{{execute}}

Download the binary for your platform:
```
export OPERATOR_SDK_DL_URL=https://github.com/operator-framework/operator-sdk/releases/latest/download
curl -LO ${OPERATOR_SDK_DL_URL}/operator-sdk_${OS}_${ARCH}
```{{execute}}

Install the release binary in your PATH
`chmod +x operator-sdk_${OS}_${ARCH} && sudo mv operator-sdk_${OS}_${ARCH} /usr/local/bin/operator-sdk`{{execute}}

Let's create a new directory for our project:

`mkdir -p $HOME/projects/podset-operator`{{execute}}

Navigate to the directory:

`cd $HOME/projects/podset-operator`{{execute}}

Initialize a new Go-based Operator SDK project for the PodSet Operator:

`operator-sdk init --domain=example.com --repo=github.com/redhat/podset-operator`{{execute}}