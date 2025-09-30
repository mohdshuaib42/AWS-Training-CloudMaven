AWS IAM and EC2 Access Setup

# IAM Users and Groups Setup
Step 1: Create IAM Group

Group Name: JuniorAdmins

Purpose: For junior administrators who need read-only access to IAM resources.

Step 2: Create a Custom IAM Policy

Policy Name: IAMReadOnlyPolicy

Permissions: Read-only access for IAM users, groups, and policies

Step 3: Attach Policy to Group

Attach IAMReadOnlyPolicy to the JuniorAdmins group.

Step 4: Create IAM User

User Name: JAdminUser1

Access Type: AWS Management Console

Add the user to the JuniorAdmins group.

Step 5: Verification

Login as JAdminUser1

✅ Can view IAM resources (users, groups, policies)

❌ Cannot create new IAM users or groups

# EC2 Access User Setup
Step 1: Create EC2 IAM User

User Name: EC2UserFullAccess

Purpose: Perform EC2-related actions only.

Step 2: Attach EC2 Policy

Permissions: Full EC2 access (ec2:*)

Constraints: Limit to a specific region and enforce resource tags.

Step 3: Test Access via AWS CLI

Configure AWS CLI with user credentials

Policies Used

IAMReadOnlyPolicy: Read-only access to IAM resources

EC2FullAccessWithRegionAndTags: Full EC2 permissions restricted to a region and requiring tags

Verification
IAM User Verification

Login as JAdminUser1

✅ Can view users, groups, policies

❌ Cannot create or modify users/groups

EC2 User Verification

Login as EC2UserFullAccess

✅ Can perform EC2 actions in allowed region with required tags

❌ Cannot perform EC2 actions outside allowed region or without tags