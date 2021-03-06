
# Building

## Hubspot

    - Sales 
        - Deals
            - Build 
To find list of current builds

## Types of Builds

- STU/ACA - Student/Academic
- STAFF - Staff
- ATH - Athletic

## Notes

Notes by {Developer}

** Build Questionare (BD.pdf) has important form information

# Create District

- New seed instillation
- Verify school/district with school address / website (nces.ed.gov)
- Check if school is public/private
- Is this an Academic district(build)?
  - No, Athletic
  - Yes, Academic
- Enter school address

## Subdomain

[district identifier]-[state-abreviation].finalforms.com
i.g. "sevenoaks-in.finalforms.com"

Check `~/finalforms/district-rails/app/forms/students/districts` for existing districts.

## Hubspot id / Education Service Center (ESC)

i.g. app.hubspot.com/.../company/xxxxxxxxxxx

## Billing

For Athelete - Per Athlete
For Academic - Per Student

Enter Rate of student/athelete from Hubspot
Enter Contact information from Hubspot

** *Phone number optional*

## Projections

Check Qty. Students/Staff and enter for Projections

## Check Notes

Make note and tag Project Manager

- Build Start
- ETA
- Missin Information

## Representative

Representative / Deal Owner / Sales Rep

## Colors

- Link Color and Icon Color should be the same
- Hover color should be lighter

## UI Builds

Terminate Server

### Dump and import umbrella database

    thor database:dump_and_import umbrella

### Dump and import the District

    thor database:dump_and_import [subdomain]_[state_initial]

### Create a branch for the build

    git checkout -b randall_[subdomain]_[state_inital]

### Create Nav-bar logo

- Logo
- Text
- Size aspects details in Documents
- Max height: 35px
- Max width: 400px
- Anchor left*

Save as in

    app/assets/images/districs/[subdomain]_[state_abreviation]/disctric/navbar-logo.png

# Creating forms for District

- Navigate to `app/forms/[student/staff]/distric`.
- Create directory named [subdomain_state]. i.g. `sevenoaks_in`
- Create a `domain` directory inside subdomain_state.
- Create imbedded ruby file with slug of the form. i.g. `student_handbook.html.erb`

## Creating script for form

- Navigate to `db/updates/build/randall`
- Create Ruby file named `subdomain-state.rb`. i.g. `sevenoaks-in.rb`

```
    Rails.logger.level = Logger::INFO
    load "#{Rails.root}/db/seeds/universal/helper.rb"

    @district = Database.connect_to "sevenoaks-in"
    @helper = SeedHelper.new @district
    @form = @helper.create_student_form(
        name: "Student Handbook Sign Off",
        categories: "athletic",
        attachable_types: %[ district ],
        position: 450,
        school_year: 2021,
    )

    @helper.create_student_form_attachments @form, "on_sports", @district, enrollment_status_filter: "allow_all"
```


## Upload Documents 

In FinalForms: 
    Schools < 
