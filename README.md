These examples demonstrate how to create a stored policy on an blob container in Azure Storage using C# and Python. The stored policy is then used to create a Shared Access Signature, which can be used to provide restricted access to the contents of the containers.

These examples were primarily created to generate SAS tokens to restrict access to blob storage containers used by HDInsight..

##How the examples work

The example code performs the following actions:

1. Creates a storage client

2. Creates (if it doesn't already exist,) a blob container

3. Uploads a file to the container

4. Creates a named security policy that grants read + list access to the container

5. Applies the policy to the container

6. Returns a SAS token that can be used for read + list only access to the container.

##To use the Visual Studio project

1. Open the project in Visual Studio

2. Right click on the __SASToken__ project in Solution Explorer, then select properties.

3. In properties, select __Settings__.

4. In settings, populate the following entries:

    * StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for. The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.
    
    * ContainerName: The container in the storage account that you want to restrict access to.
    
    * SASPolicyName: The name to use for the stored policy that will be created.
    
    * FileToUpload: The path to a file that will be uploaded to the container.
    
4. Run the project. It will open a console window and display the SAS token created using the policy. This can be used to provide read and list access to the container.

##To use the Python script

1. Open the SASToken.py file and change the following values:

    * policy\_name: The name to use for the stored policy that will be created.
    
    * storage\_account\_name: The name of your storage account.
    
    * storage\_account\_key: The key for the storage account.
    
    * storage\_container\_name: The container in the storage account that you want to restrict access to.
    
    * example\_file\_path: The path to a file that will be uploaded to the container.

2. Run the script. It will display the SAS token created using the policy. This can be used to provide read and list access to the container.

##To use the SAS token

For generic information on using these tokens, see [Shared Access Signatures part 2: Create and use a SAS with blob service](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-2). This document contains some C# code that can be used to test the signatures.

Or, if you use HDInsight, there is a sample PowerShell script in the `CreateCluster` directory that can be used, along with the SAS token information, to create a new cluster that can access the storage account using the token. The script just requires you to replace some values at the beginning, then run it to create a cluster. This allows you to restrict HDInsights access to data on that account to read/list-only.
