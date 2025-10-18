# Blockchain-EBA-Hyperledger-Fabric

This project focuses on developing Hyperledger Fabric Private Blockchain Chaincode. Hyperledger Fabric is one of the leading frameworks for permissioned blockchain which is known for its flexible architecture, scalability and detailed access control features. This project required developing and deploying a private blockchain network and a custom smart contract using Go. The main goal of this project was to simulate a supply chain management system with features to create and update products, check if a product exists and query product data. 

A smart contract named ‘SupplyChainContract’ was created in Go using the Visual Studio IDE, which was used to perform various operations on the product records on a private Hyperledger Fabric network. The contract was responsible for creating new products in the ledger, updating the products, initializing the ledger with sample products, transferring the ownership of a product and querying products from the ledger.

The code was developed in Go programming language and had the following structure:
- Product Structure: The product schema consisted of
 the ID, Name, Status, Owner, CreatedAt, UpdatedAt, Category
 and Description fields.
- Contract Implementation: The ‘SupplyChainCon
tract’ struct was built using the Fabric Contract API, and
 the business logic was added through its receiver functions
 to handle transactions.
- Ledger Initialization: The ‘InitLedger’ method was
 used to initialize the blockchain state with two predefined
 product entries. ‘GetTxTimestamp’ was used to get the times
tamps which was changed to the RFC3339 format to ensure
 that they are consistent across all the products. The helper
 function ‘putProduct’ was used to insert each product.
- Product Creation: The ‘CreateProduct’ method was
 used to create a new product with “Manufactured” status along
 with the create and update fields. The method first checks if
 the product ID is unique and only then it proceeds to create
 the product.
- Product Update: The ‘UpdateProduct’ method was
 used to update certain fields of the existing products namely
 status, category, description and the timestamp. The timestamp
 was updated to the current time as it was recorded as the last
 timestamp of the changes made.
- Ownership Transfer: The ‘TrasferOwnership’ method
 was used to reassign the owner for an existing product.
 This method was used separately and the functionality of
 transferring ownership is not included in the ‘UpdateProduct’
 method. This method also recorded the last timestamp for
 maintaining the transaction logs.
- Querying and Retrieval: The ‘QueryProduct’ method
 was used to fetch any product by its product ID. Similarly,
 the ‘GetAllProducts’ method was used to fetch all the existing
 products from the ledger. These methods are necessary in case
 we need to view the information for any product, or if we
 want to maintain the product audit for future reference and
 debugging.
- Helper Functions: There were two helper functions
 used, namely ‘putProduct’ and ‘getTimestamp’. The ‘putProd
uct’ function was used to insert the product data into the
 JSON, while the ‘getTimestamp’ function was used abstract
 the timestamp logic to maintain consistency across all trans
actional records.

 The environment for the above implementation was pre
pared by locally installing Go and Git. Next, the project
 skeleton was cloned from the GitHub repository by Pavan
 Kumar. The dependencies in the project were handled
 using the ‘go mod tidy’ and ‘go mod vendor’ commands.
 The moment the execution of the commands started, several
 issues were faced due to the usage of the Windows Operating
 System initially. Most of the commands mentioned in the
 official documentations were Linux based, and finding the
 corresponding Windows compatible commands was becoming
 difficult and time consuming to achieve. To solve this  problem, the project was implemented within a Linux virtual
 machine on the Windows host.
 
 Deployment required launching the Hyperledger Fabric test
 network via Docker Compose. A new channel named ‘my
channel’ was created using the ‘network.sh’ script, and the
 chaincode package was installed on peers from both Org1 and
 Org2. After each organization approved the chaincode, which
 was necessary to proceed, it was successfully committed to
 the channel. Environment variables for the peers and TLS
 certificates were properly set in each terminal session to ensure
 smooth communication between peers.
 
 The final testing after deployment was performed using the
 Fabric peer CLI, by invoking all the chaincode functions and
 verifying their behavior through returned payloads and success
 codes. The testing included verifying the initialized products,
 creating new products, updating the products and its metadata,
 transferring the ownership of the products, and fetching the
 existing products. Apart from testing the basic functionalities,
 certain negative test cases were also verified, such as trying
 to create duplicate entries and trying to fetch products whose
 IDs do not exist
