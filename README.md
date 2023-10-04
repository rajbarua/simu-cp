# Hazelcast Simulator Scenarios (CP)

See the `test-*.yaml` files for test specifics. Note that you will need to modify the
`inventory_plan.yaml` to allocate the appropriate number of VMs per-test; same for `hazelcast.yaml`
w.r.t. the CP member count. Everything else runs as documented
[here](https://github.com/hazelcast/hazelcast-simulator/blob/master/README.md). A quick example:

```bash
perftest run test-3member-iatomicreference-128kb-set-alter-cas-casopt.yaml
```
## My Notes
### Setup
1. Create project as `~/src/hazelcast-simulator/bin/perftest create --template cp-ec2 simu-cp`
1. Install AWS as `brew install awscli`
1. Reading [documentation](https://docs.aws.amazon.com/cli/latest/userguide/sso-configure-profile-token.html) get SSO config.
    1. Go to AWS [Login](https://hazelcast.awsapps.com/start/#/)
    1. Against the Account, click `Command line or programmatic access`
    1. Copy `SSO Start URL` and `SSO Region`
    1. Run `aws configure sso` and provide details as copied above.
    1. Best to give profile name as `default`
1. Run `~/src/hazelcast-simulator/bin/inventory apply` to create the infrastructure.
    1. `inventory_plan.yaml` uses default VPC and default internet gateway. This repo has it set for `ap-south-1` region.
1. you can ssh via `ssh -i key ubuntu@<ip>`. `<ip>` is the IP of the machine as generated in `inventory.yaml`
1. Install Java `~/src/hazelcast-simulator/bin/inventory install java` and simulator `~/src/hazelcast-simulator/bin/inventory install simulator`

### Run Tests
1. `~/src/hazelcast-simulator/bin/perftest run`
### Destroy
1. Run `~/src/hazelcast-simulator/bin/inventory destroy` to destroy the infrastructure.

