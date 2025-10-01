# terraform-oci-mysql

## Description
This Terraform module provisions an Oracle Cloud Infrastructure (OCI) MySQL DB System. It supports secure password management using OCI Vault, configurable high availability, and outputs all necessary connection details for integration.

## Requirements
- Terraform >= 0.13
- OCI Provider (oracle/oci) version 7.4.0

## Providers
- oci

## Inputs
| Name                                 | Description                                                                                                    | Type    | Default      | Required |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------|---------|--------------|----------|
| mysql_db_system_availability_domain  | MySQL db system availability domain                                                                            | string  | n/a          | yes      |
| compartment_id                       | Compartment OCID where the MySQL DB system will be created                                                     | string  | n/a          | yes      |
| mysql_shape_name                     | The shape of the MySQL DB system                                                                               | string  | "MySQL.2"   | no       |
| subnet_id                            | The OCID of the subnet where the MySQL DB system will be created                                               | string  | n/a          | yes      |
| mysql_db_system_access_mode          | The access mode for the MySQL DB system                                                                        | string  | "UNRESTRICTED" | no   |
| mysql_db_system_customer_contacts_email | Email for customer contacts                                                                                   | string  | n/a          | yes      |
| mysql_db_system_is_highly_available  | Whether the MySQL DB system is highly available                                                                | bool    | false        | no       |
| mysql_db_system_admin_password       | Admin password for the MySQL DB system. Must meet OCI requirements. Can be auto-generated if not provided.     | string  | null         | no       |
| mysql_db_system_admin_username       | Admin username for the MySQL DB system. Default is 'admin'.                                                    | string  | "admin"     | no       |
| vault_id                             | The OCID of the Vault where the admin password secret is stored                                                | string  | n/a          | yes      |

## Outputs
| Name                | Description                                  |
|---------------------|----------------------------------------------|
| access_mode         | DB system access mode                        |
| admin_username      | DB system admin username                     |
| data_storage_size_in_gb | Data storage size in GB                  |
| database_mode       | Database mode                                |
| display_name        | DB system display name                       |
| endpoints           | DB system endpoints                          |
| id                  | DB system OCID                               |
| ip_address          | DB system IP address                         |
| mysql_version       | MySQL version                                |
| port                | DB system port                               |
| data_storage        | Data storage details                         |
| secret_ocid         | Vault secret OCID for admin password         |

## Usage
```hcl
module "mysql_db_system" {
  source = "<module-path>"

  mysql_db_system_availability_domain = "<availability_domain>"
  compartment_id                      = "<compartment_ocid>"
  mysql_shape_name                    = "MySQL.2"
  subnet_id                           = "<subnet_ocid>"
  mysql_db_system_access_mode         = "UNRESTRICTED"
  mysql_db_system_customer_contacts_email = "user@example.com"
  mysql_db_system_is_highly_available = false
  vault_id                            = "<vault_ocid>"
  # Optionally provide admin password and username
  # mysql_db_system_admin_password   = "<password>"
  # mysql_db_system_admin_username   = "admin"
}
```

## License
MIT License. See [LICENSE.md](LICENSE.md) for details.

