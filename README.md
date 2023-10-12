# Hazelcast Simulator Scenarios (CP)
The project explores the performance of Hazelcast CP Subsystem. It uses [Hazelcast Simulator](https://github.com/hazelcast/hazelcast-simulator) to run the tests.
### Setup
1. Make sure you have `brew` installed. If not then install it from [here](https://brew.sh/)
1. Read the hazelcast simulator [README.md](https://github.com/hazelcast/hazelcast-simulator) to get a basic understanding of the simulator.
1. Follow the [Install](https://github.com/hazelcast/hazelcast-simulator#install) section of the simulator project. Make sure that you modify `~/.bash_profile` or `~/.zshrc` as per the instructions.
1. Install AWS as `brew install awscli`
1. For the first time login, follow the steps below ([documentation](https://docs.aws.amazon.com/cli/latest/userguide/sso-configure-profile-token.html)):
    1. For Hazelcast SSO, go to AWS [Login](https://hazelcast.awsapps.com/start/#/). You may use any other mechanism to login as well.
    1. Against the Account, click `Command line or programmatic access`
    1. Copy `SSO Start URL` and `SSO Region`
    1. Run `aws configure sso` and provide details as copied above.
    1. Best to give profile name as `default`
1. OR, if you have already executed above step once then simply run `aws sso login --profile default` to login.
1. Run `inventory apply` to create the infrastructure.
    1. `inventory_plan.yaml` uses default VPC, default internet gateway and predefined AMI. This repo has it set for `ap-south-1` region. If you running on your own region and/or account then modify the `inventory_plan.yaml` accordingly.
1. you can ssh via `ssh -i key ubuntu@<ip>`. `<ip>` is the IP of the machine as generated in `inventory.yaml`
1. Install Java `inventory install java` and simulator `inventory install simulator`

### Run Tests
1. `perftest run test-3member-iatomicreference-128kb-set-alter-cas-casopt.yaml`. There are many test files in this repo. You can run any of them.
### Destroy
1. Run `inventory destroy` to destroy the infrastructure.

### Notes
1. This project was created via command `perftest create --template cp-ec2 simu-cp`

