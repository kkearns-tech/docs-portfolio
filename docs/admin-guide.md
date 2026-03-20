
**`docs/admin-guide.md`**
```md
# Admin Guide

## Who this is for
Admins managing users, roles, and system settings.

## Setup checklist
- [ ] Create admin account
- [ ] Configure roles
- [ ] Enable SSO (optional)
- [ ] Set retention defaults

## Common tasks

### Create a user
1. Go to **Admin Console → Users**
2. Select **Create user**
3. Assign a role
4. Send invite

### Reset a password
1. Go to **Users**
2. Select the user
3. Choose **Reset password**
4. Confirm reset email delivery

### Export audit logs
1. Go to **Security → Audit Logs**
2. Filter by date range
3. Select **Export CSV**

## Troubleshooting

!!! tip "User can’t log in"
    Check role assignment, SSO status, and whether the user accepted the invite.

!!! warning "Audit log export is empty"
    Confirm date range and that events exist for the selected filters.