# Managing Team Members

This topic describes how to manage team members in the Replicated vendor portal, such as inviting and removing members, and editing permissions.

## Viewing Team Members
The [Team](https://vendor.replicated.com/team/members) page provides a list of all accounts currently associated with or invited to your team. Each row contains information about the user, including their multi-factor authentication (MFA) status and role-based access control (RBAC) role, and lets administrators take additional actions, such as remove, re-invite, and edit permissions.

## Invite Members
By default, team administrators can invite more team members to collaborate. Invited users receive an email to activate their account. The activiation link in the email is unique to the invited user. Following the activation link in the email also ensures that the invited user joins the team from which the invitation originated. 

:::note
Teams that have enforced SAML-only authentication do not use the email invitation flow described in this procedure. These teams and their users must log in through their SAML provider.
:::

To invite a new team member:

1. From the [Team Members](https://vendor.replicated.com/team/members) page, click **Invite member**.

  The Invite team member dialog opens.

1. Enter the email address of the member and their assigned RBAC policy, and click **Invite Member**.

  People invited to join your team receive an email notification to accept the invitation. They must follow the link in the email to accept the invitation and join the team. If they do not have a Replicated account already, they can create one that complies with your password policies, MFA, and Google authentication requirements. If an invited user's email address is already associated with a Replicated account, by accepting your invitation, they automatically leave their current team and join the team that you have invited them to.

## Re-invite Members

Invitations expire after 7 days. If a prospective member has not accepted their invitation in this timeframe, you can re-invite them without having to re-enter their details. You must be an administrator to perform this action.

To re-invite a prospective member:

1. Click **Reinvite** below the user's email address on the Team Members page.

1. Click **Reinvite** in the confirmation dialog.

## Remove Members and End Sessions
As a team administrator, you can remove team members, except for the account you are currently logged in with.

SAML-created users must be removed using this method to expire their existing sessions because Replicated does not support System for Cross-domain Identity Management (SCIM).

To remove a member:

1. From the Team Members page, click **Remove** on the right side of a user's row.

1. Click **Remove** in the confirmation dialog.

  The member is removed. All of their current user sessions are deleted and their next attempt at communicating with the server logs them out of their browser's session.

  For Google-authenticated users, if the user's Google account is suspended or deleted, Replicated logs that user out of all Google authenticated vendor portal sessions within 10 minutes. The user remains in the team list, but they cannot log into the vendor portal unless the username and password are allowed.
