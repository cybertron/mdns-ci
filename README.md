# mdns-ci

Scripts that can be used with Jenkins to run CI on the `openshift-metalkube/coredns-mdns`
and `openshift-metalkube/mdns-publisher` repos.

## Usage

To use these scripts, configure a `Multibranch Pipeline` job in Jenkins. Add a GitHub
`Branch Source` and configure it with the appropriate repo details.

## Other Dependencies

There must be a stackrc in `/var/lib/jenkins` that provides access to an OVB-capable
cloud. There must also be an SSH private key there which allows access to a keypair
in the target cloud called "jenkins". The private key file should be named
`id_rsa.jenkins`. This key will be used to SSH into the nodes created by OVB.

The Jenkins GitHub plugin must be properly configured for Jenkins to vote on PRs or
branches. This can be found in `Manage Jenkins->Configure System->GitHub`. On that
same configuration page, under `Lockable Resources Manager`, create a resource named
`mdns`, which will be used to prevent multiple jobs from running at once. The id of
the OVB environment is currently hard-coded, so only one job can run at once.

There are OVB configurations in `coredns-mdns-integration` that may need to be updated
to match the target cloud (images, flavors, etc.).
