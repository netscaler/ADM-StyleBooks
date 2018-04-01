# Contributing
If you want to contribute any StyleBooks you developed back to this repository, please follow the Github Pull Request model described here: https://gist.github.com/Chaser324/ce0505fbed06b947d962

Please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change. 

Please note we have a code of conduct, please follow it in all your interactions with the project.

## Pull Request Process

1. Each StyleBook set should be in its own sub-directory under the relevant category name and contain a README.md file. For example
    ```
     Authentication 
        Sample-SAML-IDP 
              saml-policy.yaml 
              auth-vserver.yaml
              saml-policy-bindings.yaml
              README.md
    ```
2. Update the README.md with the purpose of this StyleBook, and details of what configuration objects each StyleBook file creates.
3. Specify the MAS version and the NetScaler version that this StyleBook has been tested on.
4. If this is based on an existing StyleBook, specify the original StyleBook and what changes you made to it.
5. Include a display-name and description attributes in your StyleBook.
6. Mark any StyleBooks that are used as building blocks for the main StyleBook as private by setting the private attribute in these StyleBooks to true.
6. Ensure that your StyleBook follows the same style, naming conventions and formatting as Citrix Default StyleBooks.

Please note that any contributions you make to this repository are governed by the MIT License.

## Guidelines for StyleBook Authors

Here are a few guidelines to follow when writing your own StyleBooks:

1. Provide your StyleBook with a meaningful name, display-name and description. The last two are used to display your StyleBook in MAS GUI.

2. Choose a namespace for your StyleBook that is unlikely to clash with others. For example, you can use the following format "com.<your-company-name>.adc.stylebooks.<department>". Note that the namespaces "com.citrix.adc.stylebooks" and "com.citrix.adc.enterprise.stylebooks" are reserved for Citrix Default StyleBooks in MAS.

3. It is a good practice to always create at least 2 configpacks using the same StyleBook on the same NetScaler device to ensure that entities created by 2 configpacks are independent and do not conflict with each other (i.e. you are not using hardcoded names for entities in your StyleBook).

4. Whenever possible, build on top of the existing StyleBooks in MAS to simplify your own StyleBook and benefit from configurations that have already been reviewed and tested.
  
5. If several of your StyleBooks share a common set of parameters, then you can create a separate private StyleBook that contains these parameters, and then import this StyleBook wherever you need to use these parameters (see the parameters-default-sources construct in StyleBooks).

6. Always provide a label and description for your parameters, so they display correctly in MAS GUI.

7. If you have names made of multiple words, separate words with "-". For example, "vip-name".

8. For the main StyleBook, you can designate one of the parameters of your StyleBook (typically the "name" parameter or similar) as a key parameter by setting the "key" attribute to true. The value of this parameter will show up as the name of the ConfigPack in the MAS GUI.
 
9. Use lowercase for StyleBook names, parameters, components, substitutions, outputs and properties.

10. Avoid where possible using quotes or double quotes to wrap strings, as they are often not required in YAML.

11. It is a good practice to suffix the name of components with "-comp". For example a component that builds an lbvserver would be for example named "lbvserver-comp".

12. Use StyleBook references whenever possible to reference a name of another component. For example, if your StyleBook builds an lbvserver, a servicegroup, then a binding between lbvserver and servicegroup, then in the binding, do not reconstruct the names again but use references to refer to the name of the lbvserver and servicegroup of the components where they were built.

13. If the same expression or constant is used in multiple places, or for readability you want to give a mnemonic name to a long complex expression a name, use StyleBook substitutions. 

14. If your StyleBook has an Outputs section, it is good practice to pass the whole component as the output not just the property needed.

## Code of Conduct

### Our Pledge

In the interest of fostering an open and welcoming environment, we as
contributors and maintainers pledge to making participation in our project and
our community a harassment-free experience for everyone, regardless of age, body
size, disability, ethnicity, gender identity and expression, level of experience,
nationality, personal appearance, race, religion, or sexual identity and
orientation.

### Our Standards

Examples of behavior that contributes to creating a positive environment
include:

* Using welcoming and inclusive language
* Being respectful of differing viewpoints and experiences
* Gracefully accepting constructive criticism
* Focusing on what is best for the community
* Showing empathy towards other community members

Examples of unacceptable behavior by participants include:

* The use of sexualized language or imagery and unwelcome sexual attention or
advances
* Trolling, insulting/derogatory comments, and personal or political attacks
* Public or private harassment
* Publishing others' private information, such as a physical or electronic
  address, without explicit permission
* Other conduct which could reasonably be considered inappropriate in a
  professional setting

### Our Responsibilities

Project maintainers are responsible for clarifying the standards of acceptable
behavior and are expected to take appropriate and fair corrective action in
response to any instances of unacceptable behavior.

Project maintainers have the right and responsibility to remove, edit, or
reject comments, commits, code, wiki edits, issues, and other contributions
that are not aligned to this Code of Conduct, or to ban temporarily or
permanently any contributor for other behaviors that they deem inappropriate,
threatening, offensive, or harmful.

### Scope

This Code of Conduct applies both within project spaces and in public spaces
when an individual is representing the project or its community. Examples of
representing a project or community include using an official project e-mail
address, posting via an official social media account, or acting as an appointed
representative at an online or offline event. Representation of a project may be
further defined and clarified by project maintainers.

### Attribution

This Code of Conduct is adapted from the [Contributor Covenant][homepage], version 1.4,
available at [http://contributor-covenant.org/version/1/4][version]

[homepage]: http://contributor-covenant.org
[version]: http://contributor-covenant.org/version/1/4/
