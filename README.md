# circleci-cli-explore
Exploring CircleCI CLI

## Notes

Tested the following commands locally:

```console
# verifying my local CircleCI CLI version
$ circleci version
0.1.22322+5ff92b4 (homebrew)

$ circleci config validate raw.yml
Config file at raw.yml is valid.

$ circleci config process raw.yml > processed.yml

$ cat processed.yml
version: 2
jobs:
  test:
    docker:
    - image: cimg/base:current
    resource_class: small
    steps:
    - run:
        name: null
        command: |
          date

          lsb-release -d

          ssh -V
          openssl --version

          which curl
    - run:
        command: |
          echo "Current date: $(date)"

          echo "OS info: $(lsb-release -d)"

          echo "SSH and SSL versions...."
          ssh -V
          openssl --version

          echo "Checking curl version...."
          which curl
workflows:
  main:
    jobs:
    - test
  version: 2

# Original config.yml file:
# version: 2.1
#
# executors:
#   main-small:
#     docker:
#       - image: cimg/base:current
#     resource_class: small
#
# jobs:
#   test:
#     executor: main-small
#     steps:
#       - run:
#           name:
#           command: |
#             date
#
#             lsb-release -d
#
#             ssh -V
#             openssl --version
#
#             which curl
#       - run: |
#             echo \"Current date: $(date)\"
#
#             echo \"OS info: $(lsb-release -d)\"
#
#             echo \"SSH and SSL versions....\"
#             ssh -V
#             openssl --version
#
#             echo \"Checking curl version....\"
#             which curl
# workflows:
#   main:
#     jobs:
#       - test
```