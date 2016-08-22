# Rails Test App for Doorkeeper [#877](https://github.com/doorkeeper-gem/doorkeeper/issues/877)

Test app to demonstrate doorkeeper [#877](https://github.com/doorkeeper-gem/doorkeeper/issues/877).

## Setup

Run the following:
```bash
bundle install
rake db:setup
rails s
```

Then in a different console
```bash
curl http://localhost:3000/oauth/token -X POST -H "Cache-Control: no-cache" \
-F "username=test@test.com" \
-F "password=testtest" \
-F "grant_type=password"
```

Look back at the first console and there should be a stack trace that starts like:
```
ActiveModel::MassAssignmentSecurity::Error (Can't mass-assign protected attributes for Doorkeeper::AccessToken: application_id, resource_owner_id, scopes, expires_in, use_refresh_token):
  protected_attributes (1.1.0) lib/active_model/mass_assignment_security/sanitizer.rb:60:in `process_removed_attributes'
  protected_attributes (1.1.0) lib/active_model/mass_assignment_security/sanitizer.rb:10:in `sanitize'
  protected_attributes (1.1.0) lib/active_model/mass_assignment_security.rb:355:in `sanitize_for_mass_assignment'
  protected_attributes (1.1.0) lib/active_record/mass_assignment_security/attribute_assignment.rb:58:in `assign_attributes'
  protected_attributes (1.1.0) lib/active_record/mass_assignment_security/core.rb:8:in `init_attributes'
  ...
```