## STEPS TO REPRODUCE

1. Create a Scrathc Org
2. Push this repository config to it:
    - sfdx force:source:push

##Issues Noted:

1.- the Admin.profile-meta.xml contains FLS for certain custom fields, they are not applied to the sys admin profile when pushing to the scratch org
2.- this impedes me from running `sfdx force:data:tree:import --plan ./data/sample-data-plan.json` because the profile does not have edit access on the fields.
