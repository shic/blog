---
layout:     post
title:      "Backend-Tips"
date:       2016-03-20 12:00:00 
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

## Backend Hierarchy

WarehouseController

WarehouseHandler

ObjectHandler

AdvancedQueryHandler

ClientHandler



Json

JX-RS

Service

Controller

Presistence



## Add a new ES Index

We try to store a global config data in the persistence 

### Call controller to access the data 

```java
long incrementalCounter = Controllers.configs.getNextProductIncremental();
```



### Controller (Controller)

```java
/*from server/application/src/main/java/com/uper/application/ConfigController.java*/
public class ConfigController {
	private Repository repository;
	
	@Inject
	public ConfigController(Repository repository){
		this.repository = repository;
	}
	
	public long getNextProductIncremental(){
		Config config = repository.configs.get(Config.PRODUCT_INCREMENTAL);
		
		long incremental = Long.parseLong(config.getFirstValue());
		
		config.getValues().set(0, (incremental+1)+"");
		repository.configs.update(config, true);
		
		return incremental;
	}
}
```

### Add Controller to Controllers (Controller)

```java
/*from server/application/src/main/java/com/uper/application/Controllers.java*/
public class Controllers {
	public static ConfigController configs;
	
	@Inject
	public Controllers(@Named("platform.prod") boolean productionPlatorm,ConfigController configs) {
    
		Controllers.productionPlatform = productionPlatorm;
		this.configs = configs;
	}
}
```

### Add a handler (Presistence)

```java
/*from server/persistence/src/main/java/com/uper/persistence/handlers/ConfigHandler.java*/
public class ConfigHandler extends ObjectHandler<Config> implements PersistenceHandler<Config> {

	private static final Logger LOGGER = Logger.getLogger(ConfigHandler.class);
	
	public ConfigHandler(ObjectMapper mapper, Client client, String indexName, String typeName,
			boolean refresh) {
		super(mapper,client, indexName, typeName, Config.class, refresh);
	}
	
}
```

### Mapping (Presistence)

Here we decide how to store data in ES

```java
/*from server/administration/src/main/resources/es/config_mapping.json*/
{
	"properties":{
		"values":{
			"type":"string",
			"index":"not_analyzed"
		}
	}	
}
```

### Persistence (Presistence)

```java
/*from server/persistence/src/main/java/com/uper/persistence/Repository.java*/
public class Repository {
	public final ConfigHandler configs;
    @Inject
    public Repository(ConfigHandler configs) {
		super();
		this.configs = configs;
	}
}
```

###  ()???

```java
/*from server/services/src/main/java/com/uper/services/guice/ApplicationModule.java*/
public class ApplicationModule extends AbstractModule{
	@Override
	protected void configure() {
	     bind(ConfigController.class).asEagerSingleton();
	
	}
}
```

### Injection (Presistence)

Injection at runtime

```java
/*from server/services/src/main/java/com/uper/services/guice/PersistenceModule.java*/
public class PersistenceModule extends AbstractModule{
    @Provides
    public ConfigHandler providesConfigHandler(@Named(PERSISTENCE_OBJECT_MAPPER) ObjectMapper mapper, Client client,@Named("es.index.configs") String indexName){
    	return new ConfigHandler(mapper, client, indexName, "Config", false);
    }
    
}
```

### Bootstrap ES (Init ES Data)

```java
/*from server/administration/src/main/java/com/uper/administration/BootstrapES.java*/
public class BootstrapES {
	private static final String CONFIG_TYPE = "Config";
	private static final String CONFIG_INDEX = "configs";
	
	public static void main(String[] args) throws BinaryContentException, Exception {
      	//create index
		prepareIndex(client, CONFIG_INDEX, CONFIG_INDEX+VERSION, CONFIG_TYPE, "/es/general_settings_api.json", new String[]{"/es/base_entity_mapping.json","/es/config_mapping.json"});
      
      	private static void bootstrapData(Client client, ObjectMapper mapper){
      		ConfigHandler configs = new ConfigHandler(mapper, client, CONFIG_INDEX, CONFIG_TYPE, true);
          	configs.store(new Config(Config.PRODUCT_INCREMENTAL, Arrays.asList(new String[]{"8"})));
        }
    }
}


```

### Config

```java
/*from server/services/src/main/resources/config-dev.properties*/
es.index.configs=configs

/*from server/services/src/main/resources/config-prod.properties*/
es.index.configs=configs
```

### Domin

```java
/*from domain/src/main/java/com/uper/domain/Config*/

public class Config extends BaseEntity{

	public static final Id PRODUCT_INCREMENTAL = new Id("PRODUCT_INCREMENTAL");
	
	private List<String> values;

	private Config() {
		super();
	}

	public Config(Id id, DateTime creationDate, DateTime lastUpdate, List<String> values) {
		super(id, creationDate, lastUpdate);
		this.values = values;
	}

	public Config(Id id, List<String> values) {
		super(id);
		this.values = values;
	}
    
    //Do not add function setFirstValue(), because this will create a value FirstValue in persistence ???
  	public String getFirstValue(){
		return values.get(0);
	}
  
	public List<String> getValues() {
		return values;
	}
	public void setValues(List<String> values) {
		this.values = values;
	}


```



## Add a New API

### Service

```java
/*from server/services/src/main/java/com/uper/services/rest/WarehouseService.java*/
@Api(value = ServiceModule.API_PREFIX+"/warehouses", description = "Warehouse APIs")
@Path(ServiceModule.API_PREFIX+"/warehouses/")
@Produces(MediaType.APPLICATION_JSON)
@Consumes(MediaType.APPLICATION_JSON)
public class WarehouseService extends UnifiedAuthService {
    @POST
    @Path("orders/stock")
    @ApiOperation(value = "stock an order", notes = "", response = OrdersResponse.class)
    public OrdersResponse stockInOrder(OrderRequest request) throws ServerException {
    
    	authenticateForType(request.getAuth(), TYPE.WAREHOUSE);
        //remap maps Domin->DTO or DTO->Domin
    	Order order = RequestFixtures.remapOrder(request.getOrder());
    	
    	Order updatedOrder = Controllers.warehouses.stockWarehouseInOrderBox(order.getId(), order.getOrderProducts());
    	
    	return new OrdersResponse(ResponseFixtures.remapOrders(Arrays.asList(updatedOrder)),"");
    }
}
```



