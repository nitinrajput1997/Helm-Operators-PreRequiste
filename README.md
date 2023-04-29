# Helm-based-Operators

## Prerequisites

**1. Compile and install from master 

Prerequisites - git, go version 1.19
Ensure that your GOPROXY is set to "https://proxy.golang.org|direct"
```
git clone https://github.com/operator-framework/operator-sdk
cd operator-sdk
git checkout master
make install
```

**2. Install from GitHub release

Prerequisites - curl, gpg version 2.0+

1. Download the release binary
Set platform information:
```
export ARCH=$(case $(uname -m) in x86_64) echo -n amd64 ;; aarch64) echo -n arm64 ;; *) echo -n $(uname -m) ;; esac)
export OS=$(uname | awk '{print tolower($0)}')
```

Download the binary for your platform:
```
export OPERATOR_SDK_DL_URL=https://github.com/operator-framework/operator-sdk/releases/download/v1.28.1
curl -LO ${OPERATOR_SDK_DL_URL}/operator-sdk_${OS}_${ARCH}
```

2. Verify the downloaded binary
Import the operator-sdk release GPG key from keyserver.ubuntu.com:
```
gpg --keyserver keyserver.ubuntu.com --recv-keys 052996E2A20B5C7E
Download the checksums file and its signature, then verify the signature:

curl -LO ${OPERATOR_SDK_DL_URL}/checksums.txt
curl -LO ${OPERATOR_SDK_DL_URL}/checksums.txt.asc
gpg -u "Operator SDK (release) <cncf-operator-sdk@cncf.io>" --verify checksums.txt.asc
You should see something similar to the following:

gpg: assuming signed data in 'checksums.txt'
gpg: Signature made Fri 30 Oct 2020 12:15:15 PM PDT
gpg:                using RSA key ADE83605E945FA5A1BD8639C59E5B47624962185
gpg: Good signature from "Operator SDK (release) <cncf-operator-sdk@cncf.io>" [ultimate]
Make sure the checksums match:

grep operator-sdk_${OS}_${ARCH} checksums.txt | sha256sum -c -
You should see something similar to the following:

operator-sdk_linux_amd64: OK
```

3. Install the release binary in your PATH
```
chmod +x operator-sdk_${OS}_${ARCH} && sudo mv operator-sdk_${OS}_${ARCH} /usr/local/bin/operator-sdk
```
