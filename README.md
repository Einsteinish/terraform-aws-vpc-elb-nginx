# Terraform AWS vpc, elb, and nginx

This provides a template for running a simple two-tier architecture on Amazon
Web services. The premise is that we have stateless app servers running behind
an ELB serving traffic.

It does the following:

- aws_internet_gateway.default
- aws_route.internet_access
- aws_security_group.default
- aws_security_group.elb
- aws_subnet.default
- aws_vpc.default
- aws_instance.web
- aws_elb.web

To simplify the example, this intentionally ignores deploying and
getting our application onto the servers. However, we could do so either via
[provisioners](https://www.terraform.io/docs/provisioners/) and a configuration
management tool, or by pre-baking configured AMIs with
[Packer](http://www.packer.io).

This example will also create a new EC2 Key Pair in the specified AWS Region. 
The key name and path to the public key must be specified via the  
terraform command vars.

After we run `terraform apply` on this configuration, it will
automatically output the DNS address of the ELB. After our instance
registers, this should respond with the default nginx web page.

To run, configure our AWS provider as described in 

https://www.terraform.io/docs/providers/aws/index.html

Run with a command like this:

```
terraform apply -var 'key_name={your_aws_key_name}' \
   -var 'public_key_path={location_of_your_key_in_your_local_machine}'` 
```

For example:

```
terraform apply -var 'key_name=terraform' -var 'public_key_path=/Users/jsmith/.ssh/terraform.pub'
```

Cloned from [https://github.com/hashicorp/terraform/tree/master/examples/aws-two-tier](https://github.com/hashicorp/terraform/tree/master/examples/aws-two-tier).


# Tutorials

[Introduction to Terraform with AWS elb & nginx](http://bogotobogo.com/DevOps/DevOps-Terraform.php)


