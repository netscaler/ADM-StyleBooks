This folder contains a set of StyleBooks related to authentication features in NetScaler. 

You can use these StyleBooks as building blocks to create your own StyleBooks that make use of these NetScaler Auth features.

The main StyleBook file auth-v11.yaml create an authenticationvserver and binds it to any type of authentication-related policies that are passed as parameters. 


Note: The main StyleBook doesn't build the policies, it just binds them to authentication vserver. Use other StyleBooks to build the policies themselves. Some of the BusinessApps StyleBooks show how the policies can be built with these other StyleBooks and combined with the auth-v11.yaml StyleBook.

