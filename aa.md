I want you to do the following, each of the steps below need to be deeply inspected, a comprehensive plan formed and then executed. Store the aritfacts in a directory called `temp`. This should be the plan, prompt, etc that gets created from each of the steps. The final deliverable of this work should be pages in a directory called `docs/concepts` and they will be mintlify pages.

- Analyse the Getting Started section in this project so that you can get a brief understanding of what this project is about
- Anayse the UI codebase at `/Users/barenderasmus/development/examples/core` to get a good understanding of the features and capabilites on this project.
- Act as a technical copywriter and build the requirements for what contributes to good technical documentation such as audience, scope, tone, etc.
- Use the requirements from the previous step and fledge them out accroding to what this project is about and what you understood from it during the analysis phase. I want the documentation by Github, `https://docs.github.com/en/actions/concepts`, to inspire the approach, style, etc.
- Now that you have the foundation for the documentation appraoch defined, map out the best suited structure for the concepts section which will help the user understand each of the areas such as Form, Sections, Fields, etc. It needs to only cover the core aspects which will be essentail to the audience (defined earlier), to get a good grip of the basics. I needs to create the `AHA` moment. You can also use inspiration from Kubernetes, Helm and other YAML based products to see how they structure it. I don't want it be be overly technical, overengineered, many bullet points, etc. I want it to be understandable, logical and provide the user with a good base to start with. 
- Lastly, define a review and validation step which reviews the content produced to ensure it aligns with the requirements/specific set out initially, and if there's any changes that needs to be made, do so. You should also fact check against the codebase to ensure that what is describe is accurate and true.







I just want to clarify something for the fields section, for example, I don't want to extensively list all the field types and cover any of the field types in depth. It needs to be mainly around fields as a concept rather than the specifics, what fields can offer because they are quite diverse. And then when it comes to the connections, you might also need to inspect the API project in order to get a better understanding of how the connections work. Just to give you a short summary, for example, the Airtable connection, the user will need to navigate to a OAuth URL, which you can find in the UI or core project. And then you can see it will redirect the user and ultimately show them a page with a modal or some form with a connection ID, which will then be a reference or need to be used alongside the Airtable connection. Make sure you have a good understanding of these things before you write the documentation.

Here is the API project repository `/Users/barenderasmus/development/examples/api`











I want you to review and then refine the concepts section that you have just created. So overall, I like the style and the method that it is documented, but how I would like it to flow is Forms being the first section, and you can explain the core concepts of the form, like you have, and then when you move to sections, you can explain it with the primary objective of there being to show how you can have a single section form as well as a multiple section form, and maybe perhaps covering a brief explanation of how the form would flow. Then the next step would be perhaps conditional or would be fields, sorry. So fields, you would explain in the same way, kind of just explaining the core, building on top of the fact that the user has just come from the sections concept page. Then next could be connections or even completion screen. You can even then go into, say, cover some of the details such as start date and end date, and that can maybe be covered in the forms page itself. But something like analytics, so the mix panel stuff will be covered in its separate page. And once the user fully understands the forms, the fields, the section, maybe validation can go right below fields as a following section. And again, you can just explain it in the core. But once the user has a basic understanding of those type of things, then you can start covering conditional logic, which would first include conditional routing, so branching between sections, and then perhaps followed by the visible when at a field level. The reason for this is, the main objective of the concepts is to initially just get the user up to speed with the basics so that they have a good overall understanding. And then as we progress through the concepts, things would become a little bit more complicated and more advanced.
Ideally, I want all the core properties of the YAML to be covered in the concept pages. The only ones that should be excluded is the fields and the field types where they have very specific properties that are only relevant to them. So when it comes to the form and the section, completion screen, connections, all of these things needs to be covered to a full extent, but still keeping the approach that you have taken and the style. The same for validation, that needs to be covered to quite a large extent.Before you start executing, I want to make sure that you follow the similar steps that I've previously included, where you firstly do analysis and at the end you also have a review and validation step. Make sure you also stick to the requirements as you have outlined and the research that you have done.




I've reviewed the concept pages you've created and identified the following:

- The pages aren't consistent with one another, they follow different structures
- Each pages doesn't focus on the core of the topic it's covering, for example, the forms page, has the sections in the YAML instead of being ommited like in other pages.
- The pages arent focus on explain the concepts well, for example, date boundaries are very poorly explained.
- The order of the concepts are not ideal, they need to make sense and follow logically to what the reader will expect.

I want you to review the pages yourself and take my feedback into account. Then I want you to create a core plan about the underlying issues which will help with the feedback I provided. Dont make unnessary changes such as tone, and style unless it helps address some of the feedback I've given. As a suggestion, take each of the feedback points I mentioned and analyse them, come up with 3 suggestions to address it and then pick the best one. A note from me, I want to concept pages to follow a consistent layout.

After you've made these changes, I want you to review and validate by doing the following. Act as a technical user, and start reading the first concept page, if you have any questions or something is unclear, note it down. Continue reading the pages and keep notes. At the end, review all of the notes, and use it to see if you need to add anything to any exisitng page, or even create a new page(s) to will a gap with could help the reader. 






I've again review the pages you have created and have the following feedback:

- I want each of the pages to have a consistent structure
    - The title should be the concept such as form, sections, fields, localization, etc
    - The description should be a short description of what it is, it should be understandable without context.
    - The page should then have a introduction describing that the concept is, should not be technical but focused on explaining the concept to the user so that they get the AHA-moment and feel confident in use the concept.
    - Next the page should have a section called Structure which is a narrow view of the concept it covers. Ommit the sections or details that is not covered as part of this page. 
    - Lastly, the page should explain each of the properties that is showed in the Structure section YAML. The explaination again needs to be understandable to the audience and give them the confidence to use it.
    - The page should not include any references to other sections or mentions of it. 
    - For pages like validation and connections where there are sub concepts or multiple steps such as the different connections or different validation steps, you should follow a similar structure to the main page but just in a sub section manner.

For the fields concept page, I only want you to cover the core of the field schema, this exclude thes options property which is specific to a given field type.

Perhaps another concept to cover would be templating, this can be done simirly to localization, meaning any string can be treated as a template and will be handled by handlebars. If you need more clarity on this, you can analyse the project at `/Users/barenderasmus/development/examples/core`

Here is a correction for the connections page, in order to obtain a connection ID, the user will need to navigate to the `https://app.declarativeforms.com/oauth/airtable` for example which will redirect the user to airtable and then ask them to sign in before redirecting back to the platform to show it their connection ID.





I want you to use the `test/SKILL.md` and `test/style-rules.md` along with the core project at `/Users/barenderasmus/development/examples/core` to create the best skill or multiple skills which I can use to write content for this products documentation pages. Strictly stick to the rules and guidelines in the test directory but use the core repository to understand the product better and make the require adjustments.



I want you to take each of these tasks below and understand them in detail by expanding them an creating an execution plan with a validation plan. Each of them need to be executed to the best of your ablity. Each of them should also consider to following tasks since they depend on each other.

- Research the requirements which a copywriter would need in order to write good consistent copy for a product.
- Use the research and map out the topics and touchpoints that a copywriter would need.
- Review both the marketing content and technical documentation of Kubernetes to fullfil these touchpoints which will be used to write marketing copy and technical documentation for a given product.
- Deeply inspect this repository, `/Users/barenderasmus/development/examples/core`, from a product point of view so that you can get a good understand of what this product is about.
- Review the topics and touchpoints you have define in context of the research about the prodcut you have done and make any adjustments or improvement where needed. Don't include exact product details as you can always inspect the product in future to understand the revelant area. I want you to focus on the copywriting side of things. The objective is to create a blueprint for both writing marketing relatd content and technical documentation similary to Kubernetes but applicable to this product called Declarative forms.
- Finalize the copywriting blueprint and save it in a file called `copywriting_blueprint.md`.
- Now that you have a copywriting blueprint, create a draft for the introduction.mdx and quickstart.mdx based on your understanding of the product and then use the copywriting_blueprint to refine it. 
- Next, create a draft for the concept called sections.mdx and then use the blueprint to refine it, the getting-started section will be baised towards marketing while the concepts directory will be bias towards technical style.

Next, I want you to identify all the other concepts by researching the `/Users/barenderasmus/development/examples/core` project. Once you have an extensive list of the concepts which you should cover, write the concept pages for each following the guidelines in the copywriting_blueprint.md