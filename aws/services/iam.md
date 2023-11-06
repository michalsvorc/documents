# IAM

- [Resources](https://aws.amazon.com/iam/resources/)
  - [User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)
  - [API Reference](https://docs.aws.amazon.com/IAM/latest/APIReference/)

## Roles

- [Roles terms and concepts](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html)

## IAM Identity Center (SSO) 

- [Resources](https://aws.amazon.com/iam/identity-center/resources/)
  - [User Guide](https://docs.aws.amazon.com/singlesignon/latest/userguide/)
  - [API Reference](https://docs.aws.amazon.com/singlesignon/latest/APIReference/)

### AWS Organizations (accounts)

- [Resources](https://aws.amazon.com/organizations/resources/)
- [AWS accounts](https://us-east-1.console.aws.amazon.com/organizations/v2/home/accounts)

Your AWS account must be managed by AWS Organizations to use IAM Identity Center.

When you enable IAM Identity Center for the first time, it is automatically configured with an Identity Center directory as your default identity source.

### Administrator

- [Create an administrative permission set](https://docs.aws.amazon.com/singlesignon/latest/userguide/get-started-create-an-administrative-permission-set.html)
- [Least-privilege permissions](https://docs.aws.amazon.com/singlesignon/latest/userguide/get-started-create-permission-set-to-grant-least-privilege-permissions.html)

After you choose your identity source, you'll create or specify a user and assign them administrative permissions to your AWS account.

Permission sets are stored in IAM Identity Center and define the level of access that users and groups have to an AWS accounts.

The default settings grant full access to AWS services and resources using the AdministratorAccess predefined permission set. The predefined AdministratorAccess permission set uses the AdministratorAccess AWS managed policy.

When you sign in, the name of the permission set to which the user is assigned appears as an available role in the AWS access portal.

After you create your administrative user, create a more restrictive permission set and assign it to the same user
(Least-privilege permissions).

### Multi-account permissions

With multi-account permissions you can plan for and centrally implement IAM permissions across multiple AWS accounts at one time without needing to configure each of your accounts manually. You can create fine-grained permissions based on common job functions or define custom permissions that meet your security needs. You can then assign those permissions to workforce users to control their access over specific accounts.

### Permission sets

- [User Guide](https://docs.aws.amazon.com/singlesignon/latest/userguide/permissionsetsconcept.html)
- [Assign permission set to user](https://docs.aws.amazon.com/singlesignon/latest/userguide/useraccess.html)

To enable other users to access your accounts and applications, and to administer IAM Identity Center, create and assign permission sets only through IAM Identity Center.

You can assign multiple permission sets to the same user.
