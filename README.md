# mdns-ci

Scripts that can be used with Jenkins to run CI on the openshift-metalkube/coredns-mdns
and openshift-metalkube/mdns-publisher repos.

## Usage

The two scripts must be placed in `/var/lib/jenkins/scripts`. Then configure the Jenkins
job to run `coredns-mdns-integration`. That script will stand up an OVB environment and
copy the `coredns-mdns-build` script to the "undercloud" and then run it.

`coredns-mdns-integration` takes one parameter, which is the name of the repo under
test. For example, to test coredns-mdns, the Jenkins job should be configured to call
`/var/lib/jenkins/scripts/coredns-mdns-integration coredns-mdns`.

Note that the Jenkins job must also be configured to check the repo under test out
to a `src` subdirectory in the workspace.

## Other Dependencies

There must be a stackrc in `/var/lib/jenkins` that provides access to an OVB-capable
cloud. There must also be an SSH private key there which allows access to a keypair
in the target cloud called "jenkins". The private key file should be named
`id_rsa.jenkins`. This key will be used to SSH into the nodes created by OVB.

There are OVB configurations in coredns-mdns-integration that may need to be updated
to match the target cloud (images, flavors, etc.).

Also, be aware that the id of the OVB environment is currently hard-coded, so it is
only possible to run one job at a time in a single tenant. This could be fixed, but
for the moment there isn't enough activity on these repos to require parallel jobs.
