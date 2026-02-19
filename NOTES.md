I want you to carefully review my request. I want you to make the following changes. Below are sections with details describing what I want to achieve. You should review each of these sections one by one and develop a robust plan for each of them. Once you have created the plan, you need to review each section along side the other section to ensure they are consistent. After that you can implemented. Lastly you need to review.

In instances where you need to structure or order things, make sure they are logical and correctly place. Think of it as to how a engineer or slightly technical person would like to use this documentation.

As a final request, I want you to write a CLAUDE.md file which will be use in future to make changes, improvements, add new sections, etc. that align with how I describe this task. I want to add new fields or features to this project and have the documentation written without needing to specify all of the style, practices, etc. again. Capture this in the CLAUDE.md file.

Just for reference, here is the repositories you can use

- /Users/barenderasmus/development/examples/api
- /Users/barenderasmus/development/examples/core
- /Users/barenderasmus/development/examples/examples

## Introduction

This product bas been developed since more developer focused tools are config based, such as terraform, etc. but for some reason there doesn't exist such interface for forms/surveys. With the era of LLMs such as Claude Code, Codex, and other this is becoming a bigger problem. How can I create forms using these tools? Tally, YouForm, Jotform, Google Forms, non of them support it, they don't even support a good API for creating and managing forms and force me to work through their form builder. This is great for non technical people but where everyone is starting to be able to build technical products without knowing much, this gap is emphasised.

## Quick Start

For the quickstart, I want it to be simple yet show the capabilieties of the product. Start with a good example such as a rental application form. For the quickstart, only use a few essential fields such as a short_text, single_select, and or email. Don't use this exact example. Use it along with the broader context to find the best example to serve as a use case. In the quickstart, the main objective is to just get them start. Just enough to make them curious and not too much to make them feel overwelhmed.

## How it works

You can run through the quickstart and explain it in more detail.


## Concepts > YAML Schema

Here you can cover the root properties, such as version, title, description, sections, connections, localizations, start_date, end_date, and mixpanel. Cover them in the context of the example we're using so that the reader can reference and understand. Don't cover advanced features such as localization and templating as they will be covered elsewhere. This should be just enough to help them understand the basic of the schema. 

## Concepts > Version, Title, Description

Here you need to cover the full extend of each of them which includes localization.

## Concepts > Sections

Here you need to cover sections to the full extent, all the features and all the variations. This includes each property on the section and the various ways they can function. It does not include the fields or their functionality.

## Concepts > Fields

Here you need to cover the shared properities and functionality of fields to the full extent. This includes, label, id, validators, etc but does not include the otp or options which is specific for a given field type.

## Concepts > Connections

Here you need to cover the full extent of all the connections. For the connections like Airtable, the user needs to navigate to `/oauth/airtable` in order to be redirected to start the Oauth2 flow. Make sure you cover each connection to it's full extent. This includes localization and templating, etc.

## Concepts > Localization

Localization is cover is all other sections where they are applicable but here you have a bit more of a high level and generic focus. This should focus on the core of localization rather than how it's implemented for each of the othern components. Make sure you cover it extensively.

## References > YAML Schema Reference

Only include the core properties. You can exclude the fields that are specific to a field type or to a specific scenario. Make sure it's extensive about the core/key properties to serve as a reference.

## Reference > short_text

Here you need to capture the full extent of the short_text field type and all of it's variantions. 

## Reference > long_text

Here you need to capture the full extent of the long_text field type and all of it's variantions. 

## Reference > multiple_select

Here you need to capture the full extent of the multiple_select field type and all of it's variantions. 

## Reference > single_select

Here you need to capture the full extent of the single_select field type and all of it's variantions. 

## Reference > dropdown

Here you need to capture the full extent of the dropdown field type and all of it's variantions. 
