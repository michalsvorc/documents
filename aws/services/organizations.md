# Organizations

- [User guide](https://docs.aws.amazon.com/organizations/latest/userguide)

Dashboards:

- [Organizations](https://console.aws.amazon.com/organizations/)
- [IAM Identity Center (SSO)](https://console.aws.amazon.com/singlesignon)
- [IAM (users, roles, groups)](https://console.aws.amazon.com/iamv2)

The organization's `management account` is responsible for paying the bills for all accounts in the organization.

## AWS accounts

AWS deletes all resources in the account and the account becomes unrecoverable 90 days after it's suspended.

### New account

- [User guide](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_create.html)

For Email address of the account's owner, enter the email address of the account's owner.
This email address cannot already be associated with another AWS account because it becomes the user name credential for the root user of the account.

For IAM role name, we recommend that you use the default name across all of your accounts for consistency.

### Quotas

- [Quota exceeded](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_troubleshoot_general.html#troubleshoot_general_error-adding-account)
- [Maximum and minimum values](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_reference_limits.html#min-max-values)

Before you close or delete an AWS account, remove it from your organization so that it doesn't continue to count against your quota.
