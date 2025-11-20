# Nuon AWS Empty Sandbox

This is a baseline sandbox that provides a bare minimum AWS environment for use with Nuon.

It includes outputs required for Nuon to function.

Updated 2025-08-21 to let an AWS Lambda app config work correctly. See the
[example-app-configs](https://github.com/nuonco/example-app-configs) repository for more information and other app
configs.

## Requirements

| Name                                                                     | Version   |
| ------------------------------------------------------------------------ | --------- |
| <a name="requirement_terraform"></a> [terraform](#requirement_terraform) | >= 1.7.5  |
| <a name="requirement_aws"></a> [aws](#requirement_aws)                   | >= 5.86.1 |

## Providers

| Name                                             | Version   |
| ------------------------------------------------ | --------- |
| <a name="provider_aws"></a> [aws](#provider_aws) | >= 5.86.1 |

## Modules

| Name                                         | Source                        | Version  |
| -------------------------------------------- | ----------------------------- | -------- |
| <a name="module_ecr"></a> [ecr](#module_ecr) | terraform-aws-modules/ecr/aws | >= 2.4.0 |

## Resources

| Name                                                                                                                                                            | Type        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| [aws_iam_policy.ecr_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy)                                             | resource    |
| [aws_iam_role_policy_attachment.ecr_access_deprovision](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource    |
| [aws_iam_role_policy_attachment.ecr_access_maintenance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource    |
| [aws_iam_role_policy_attachment.ecr_access_provision](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment)   | resource    |
| [aws_route53_record.caa](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record)                                            | resource    |
| [aws_route53_zone.internal](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_zone)                                           | resource    |
| [aws_route53_zone.public](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_zone)                                             | resource    |
| [aws_availability_zones.available](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones)                           | data source |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity)                                   | data source |
| [aws_iam_policy_document.ecr](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document)                               | data source |
| [aws_security_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/security_group)                                     | data source |
| [aws_security_groups.runner](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/security_groups)                                    | data source |
| [aws_subnet.private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnet)                                                     | data source |
| [aws_subnet.public](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnet)                                                      | data source |
| [aws_subnet.runner](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnet)                                                      | data source |
| [aws_subnets.private](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnets)                                                   | data source |
| [aws_subnets.public](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnets)                                                    | data source |
| [aws_subnets.runner](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnets)                                                    | data source |
| [aws_vpc.vpc](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/vpc)                                                               | data source |

## Inputs

| Name                                                                                                      | Description                                                                                                                | Type       | Default                | Required |
| --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------------------- | :------: |
| <a name="input_additional_tags"></a> [additional_tags](#input_additional_tags)                            | Extra tags to append to the default tags that will be added to install resources.                                          | `map(any)` | `{}`                   |    no    |
| <a name="input_deprovision_iam_role_arn"></a> [deprovision_iam_role_arn](#input_deprovision_iam_role_arn) | The deprovision IAM Role ARN                                                                                               | `string`   | n/a                    |   yes    |
| <a name="input_enable_nuon_dns"></a> [enable_nuon_dns](#input_enable_nuon_dns)                            | Whether or not the app should use a nuon-provided nuon.run domain. Controls the cert-manager-issuer and the route_53_zone. | `string`   | `"false"`              |    no    |
| <a name="input_internal_root_domain"></a> [internal_root_domain](#input_internal_root_domain)             | The internal root domain.                                                                                                  | `string`   | n/a                    |   yes    |
| <a name="input_kyverno_policy_dir"></a> [kyverno_policy_dir](#input_kyverno_policy_dir)                   | Path to a directory with kyverno policy manifests.                                                                         | `string`   | `"./kyverno-policies"` |    no    |
| <a name="input_maintenance_iam_role_arn"></a> [maintenance_iam_role_arn](#input_maintenance_iam_role_arn) | The provision IAM Role ARN                                                                                                 | `string`   | n/a                    |   yes    |
| <a name="input_nuon_id"></a> [nuon_id](#input_nuon_id)                                                    | The nuon id for this install. Used for naming purposes.                                                                    | `string`   | n/a                    |   yes    |
| <a name="input_prefix_override"></a> [prefix_override](#input_prefix_override)                            | The resource prefix to override, otherwise defaults to the nuon install id                                                 | `string`   | `""`                   |    no    |
| <a name="input_provision_iam_role_arn"></a> [provision_iam_role_arn](#input_provision_iam_role_arn)       | The maintenance IAM Role ARN                                                                                               | `string`   | n/a                    |   yes    |
| <a name="input_public_root_domain"></a> [public_root_domain](#input_public_root_domain)                   | The public root domain.                                                                                                    | `string`   | n/a                    |   yes    |
| <a name="input_region"></a> [region](#input_region)                                                       | The region to launch the cluster in.                                                                                       | `string`   | n/a                    |   yes    |
| <a name="input_tags"></a> [tags](#input_tags)                                                             | List of custom tags to add to the install resources. Used for taxonomic purposes.                                          | `map(any)` | n/a                    |   yes    |
| <a name="input_vpc_id"></a> [vpc_id](#input_vpc_id)                                                       | The ID of the AWS VPC to provision the sandbox in.                                                                         | `string`   | n/a                    |   yes    |

## Outputs

| Name                                                        | Description                                                                                                                                                            |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <a name="output_account"></a> [account](#output_account)    | A map of AWS account attributes: id, region.                                                                                                                           |
| <a name="output_ecr"></a> [ecr](#output_ecr)                | A map of ECR attributes: repository_url, repository_arn, repository_name, registry_id, registry_url.                                                                   |
| <a name="output_nuon_dns"></a> [nuon_dns](#output_nuon_dns) | A map of Nuon DNS attributes: whether DNS has been enabled; AWS Route 53 details for the public_domain and internal_domain.                                            |
| <a name="output_vpc"></a> [vpc](#output_vpc)                | A map of vpc attributes: name, id, cidr, azs, private_subnet_cidr_blocks, private_subnet_ids, public_subnet_cidr_blocks, public_subnet_ids, default_security_group_id. |
