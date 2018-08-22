# Cosmos-DB-using-Power-Shell

Create cosmos DB account from portal and copy primary/secondary key and use in below script

```$primaryKey = ConvertTo-SecureString -String '6uTeQahS3a7P53JBjBkyjiS3MHMEBjdLA4K8Ltav3xkRl8Iz4sW5kJpjErJSEdogROjJhZecKCdcAZ5hWJPujA==' -AsPlainText -Force```

Create Database 

```$cosmosDbContext = New-CosmosDbContext -Account 'apicosmos' -ResourceGroup 'myresource'```

```New-CosmosDbDatabase -Context $cosmosDbContext -Id 'testdb'```

Create Context

```$cosmosDbContext = New-CosmosDbContext -Account 'apicosmos' -Database 'testdb' -ResourceGroup 'myresource'```

Create New Collection in testdb with partitionkey='AlertType' and Fixed Size throughtput 
```New-CosmosDbCollection -Context $cosmosDbContext -Id 'alerts' -OfferThroughput 1000 -PartitionKey 'alertType'```

Create New Collection in testdb with partitionkey='AlertType', Fixed Size throughtput and set TTL
```New-CosmosDbCollection -Context $cosmosDbContext -Id 'events' -OfferThroughput 1000 -PartitionKey 'serialNumber' -DefaultTimeToLive 604800```


# Insert Document

```$cosmosDbContext = New-CosmosDbContext -Account 'apicosmos' -Database 'amsdb' -ResourceGroup 'myresource'

$document = @"
{
	 "id": "$([Guid]::NewGuid().ToString())",
    "name": "nogps1",
    "type": "nogps"
    "status": "ACTIVE",
	  "applicationName": "Eroutes"
}
"@

New-CosmosDbDocument -Context $cosmosDbContext -CollectionId 'miscellaneous' -DocumentBody $document

```

