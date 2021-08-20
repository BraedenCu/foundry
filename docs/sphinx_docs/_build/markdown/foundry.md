# foundry package

## Submodules

## foundry.foundry module


### class foundry.foundry.Foundry(no_browser=False, no_local_server=False, index='mdf-test', authorizers=None, \*, dc: Dict = {}, mdf: Dict = {}, dataset: foundry.models.FoundryDataset = {}, config: foundry.models.FoundryConfig = FoundryConfig(dataframe_file='foundry_dataframe.json', data_file='foundry.hdf5', metadata_file='foundry_metadata.json', destination_endpoint=None, local=False, metadata_key='foundry', organization='foundry', local_cache_dir='./data'), dlhub_client: Any = None, forge_client: Any = None, connect_client: Any = None, xtract_tokens: Any = None)
Bases: `foundry.models.FoundryMetadata`

Foundry Client Base Class
TODO:
——-
Add Docstring


#### build(spec, globus=False, interval=3, file=False)
Build a Foundry Data Package
:param spec: dict or str (relative filename) of the data package specification
:type spec: multiple
:param globus: if True use Globus to fetch datasets
:type globus: bool
:param interval: Polling interval on checking task status in seconds.
:type interval: int
:param type: One of “file” or None
:type type: str


* **Returns**

    **(Foundry)**



* **Return type**

    self: for chaining



#### check_model_status(res)
Check status of model or function publication to DLHub

TODO: currently broken on DLHub side of things


#### check_status(source_id, short=False, raw=False)
Check the status of your submission.


* **Parameters**

    
    * **source_id** (*str*) – The `source_id` (`source_name` + version information) of the
    submission to check. Returned in the `res` result from `publish()` via MDF Connect Client.


    * **short** (*bool*) – When `False`, will print a status summary containing
    all of the status steps for the dataset.
    When `True`, will print a short finished/processing message,
    useful for checking many datasets’ status at once.
    **Default:** `False`


    * **raw** (*bool*) – When `False`, will print a nicely-formatted status summary.
    When `True`, will return the full status result.
    For direct human consumption, `False` is recommended.
    **Default:** `False`



* **Returns**

    The full status result.



* **Return type**

    If `raw` is `True`, *dict*



#### collect_dataframes(packages=[])
Collect dataframes of local data packages
:param packages: List of packages to collect, defaults to all
:type packages: list


* **Returns**

    **(tuple)**



* **Return type**

    Tuple of X(pandas.DataFrame), y(pandas.DataFrame)



#### configure(\*\*kwargs)
Set Foundry config
:keyword file: Path to the file containing
:kwtype file: str
:keyword (default: self.config.metadata_file)

dataframe_file (str): filename for the dataframe file default:”foundry_dataframe.json”
data_file (str): : filename for the data file default:”foundry.hdf5”
destination_endpoint (str): Globus endpoint UUID where Foundry data should move
local_cache_dir (str): Where to place collected data default:”./data”


* **Returns**

    **(Foundry)**



* **Return type**

    self: for chaining



#### connect_client(: Any)

#### describe_model()

#### dlhub_client(: Any)

#### download(globus=True, verbose=False, \*\*kwargs)
Download a Foundry dataset
:param globus: if True, use Globus to download the data else try HTTPS
:type globus: bool
:param verbose: if True print out debug information during the download
:type verbose: bool


* **Returns**

    **(Foundry)**



* **Return type**

    self: for chaining



#### forge_client(: Any)

#### get_keys(type=None, as_object=False)
Get keys for a Foundry dataset


* **Parameters**

    
    * **type** (*str*) – The type of key to be returned e.g., “input”, “target”


    * **as_object** (*bool*) – When `False`, will return a list of keys in as strings
    When `True`, will return the full key objects
    **Default:** `False`


Returns: (list) String representations of keys or if `as_object`

    is False otherwise returns the full key objects.


#### get_packages(paths=False)
Get available local data packages


* **Parameters**

    **paths** (*bool*) – If True return paths in addition to package, if False return package name only



* **Returns**

    **(list)**



* **Return type**

    List describing local Foundry packages



#### list()
List available Foundry data packages


* **Returns**

    **(pandas.DataFrame)**



* **Return type**

    DataFrame with summary list of Foundry data packages including name, title, and publication year



#### load(name, download=True, globus=True, verbose=False, metadata=None, authorizers=None, \*\*kwargs)
Load the metadata for a Foundry dataset into the client
:param name: Name of the foundry dataset
:type name: str
:param download: If True, download the data associated with the package (default is True)
:type download: bool
:param globus: If True, download using Globus, otherwise https
:type globus: bool
:param verbose: If True print additional debug information
:type verbose: bool
:param metadata: **For debug purposes.** A search result analog to prepopulate metadata.
:type metadata: dict


* **Keyword Arguments**

    **interval** (*int*) – How often to poll Globus to check if transfers are complete



* **Returns**

    


* **Return type**

    self



#### load_data(source_id=None, globus=True)
Load in the data associated with the prescribed dataset

Tabular Data Type: Data are arranged in a standard data frame
stored in self.dataframe_file. The contents are read, and

File Data Type: <<Add desc>>

For more complicated data structures, users should
subclass Foundry and override the load_data function


* **Parameters**

    
    * **inputs** (*list*) – List of strings for input columns


    * **targets** (*list*) – List of strings for output columns


Returns
——-s

> (tuple): Tuple of X, y values


#### publish(foundry_metadata, data_source, title, authors, update=False, publication_year=None, \*\*kwargs)
Submit a dataset for publication
:param foundry_metadata: Dict of metadata describing data package
:type foundry_metadata: dict
:param data_source: Url for Globus endpoint
:type data_source: string
:param title: Title of data package
:type title: string
:param authors: List of data package author names e.g., Jack Black

> or Nunez, Victoria


* **Parameters**

    
    * **update** (*bool*) – True if this is an update to a prior data package
    (default: self.config.metadata_file)


    * **publication_year** (*int*) – Year of dataset publication. If None, will
    be set to the current calendar year by MDF Connect Client.
    (default: $current_year)



* **Keyword Arguments**

    
    * **affiliations** (*list*) – List of author affiliations


    * **tags** (*list*) – List of tags to apply to the data package


    * **short_name** (*string*) – Shortened/abbreviated name of the data package


    * **publisher** (*string*) – Data publishing entity (e.g. MDF, Zenodo, etc.)



* **Returns**

    **(dict) MDF Connect Response** – of dataset. Contains source_id, which can be used to check the
    status of the submission



* **Return type**

    Response from MDF Connect to allow tracking



#### publish_model(options)
Submit a model or function for publication
:param options: dict of all possible options

Options keys:

    title (req)
    authors (req)
    short_name (req)
    servable_type (req) (“static method”, “class method”,

    > “keras”, “pytorch”, “tensorflow”, “sklearn”)

    affiliations
    domains
    abstract
    references
    requirements (dict of library:version keypairs)
    module (if Python method)
    function  (if Python method)
    inputs (not needed for TF) (dict of options)
    outputs (not needed for TF)
    methods (e.g. research methods)
    DOI
    publication_year (advanced)
    version (advanced)
    visibility (dict of users and groups, each a list)
    funding reference
    rights

    TODO:
    alternate identifier (to add an identifier of this artifact in another service)
    add file
    add directory
    add files


#### run(name, inputs, \*\*kwargs)
Run a model on data


* **Parameters**

    
    * **name** (*str*) – DLHub model name


    * **inputs** – Data to send to DLHub as inputs (should be JSON serializable)



* **Returns**

    


* **Return type**

    Returns results after invocation via the DLHub service



* Pass 

```
**
```

kwargs through to DLHub client and document kwargs


#### xtract_tokens(: Any)

### foundry.foundry.is_doi(string: str)

### foundry.foundry.is_pandas_pytable(group)
## foundry.models module


### class foundry.models.FoundryConfig(\*, dataframe_file: str = 'foundry_dataframe.json', data_file: str = 'foundry.hdf5', metadata_file: str = 'foundry_metadata.json', destination_endpoint: str = None, local: bool = False, metadata_key: str = 'foundry', organization: str = 'foundry', local_cache_dir: str = './data')
Bases: `pydantic.main.BaseModel`

Foundry Configuration
Configuration information for Foundry Dataset


* **Parameters**

    
    * **dataframe_file** (*str*) – Filename to read dataframe contents from


    * **metadata_file** (*str*) – Filename to read metadata contents from defaults to reading for MDF Discover


    * **destination_endpoint** (*str*) – Globus endpoint ID to transfer data to (defaults to local GCP installation)


    * **local_cache_dir** (*str*) – Path to local Foundry package cache



#### data_file(: Optional[str])

#### dataframe_file(: Optional[str])

#### destination_endpoint(: Optional[str])

#### local(: Optional[bool])

#### metadata_file(: Optional[str])

#### metadata_key(: Optional[str])

#### organization(: Optional[str])

### class foundry.models.FoundryDataset(\*, keys: List[foundry.models.FoundryKey] = None, splits: List[foundry.models.FoundrySplit] = None, data_type: foundry.models.FoundryDatasetType = None, short_name: str = '', dataframe: Any = None, task_type: List[str] = [], domain: List[str] = [], n_items: int = 0)
Bases: `pydantic.main.BaseModel`

Foundry Dataset
Schema for Foundry Datasets. This includes specifications of inputs, outputs, type, version, and more


#### class Config()
Bases: `object`


#### arbitrary_types_allowed( = True)

#### data_type(: foundry.models.FoundryDatasetType)

#### dataframe(: Optional[Any])

#### domain(: Optional[List[str]])

#### keys(: List[foundry.models.FoundryKey])

#### n_items(: Optional[int])

#### short_name(: Optional[str])

#### splits(: Optional[List[foundry.models.FoundrySplit]])

#### task_type(: Optional[List[str]])

### class foundry.models.FoundryDatasetType(value)
Bases: `enum.Enum`

Foundry Dataset Types
Enumeration of the possible Foundry dataset types


#### files( = 'files')

#### hdf5( = 'hdf5')

#### other( = 'other')

#### tabular( = 'tabular')

### class foundry.models.FoundryKey(\*, key: List[str] = [], type: str = '', filter: str = '', units: str = '', description: str = '', classes: List[foundry.models.FoundryKeyClass] = None)
Bases: `pydantic.main.BaseModel`


#### classes(: Optional[List[foundry.models.FoundryKeyClass]])

#### description(: Optional[str])

#### filter(: Optional[str])

#### key(: List[str])

#### type(: str)

#### units(: Optional[str])

### class foundry.models.FoundryKeyClass(\*, label: str = '', name: str = '')
Bases: `pydantic.main.BaseModel`


#### label(: str)

#### name(: str)

### class foundry.models.FoundryMetadata(\*, dc: Dict = {}, mdf: Dict = {}, dataset: foundry.models.FoundryDataset = {}, config: foundry.models.FoundryConfig = FoundryConfig(dataframe_file='foundry_dataframe.json', data_file='foundry.hdf5', metadata_file='foundry_metadata.json', destination_endpoint=None, local=False, metadata_key='foundry', organization='foundry', local_cache_dir='./data'))
Bases: `pydantic.main.BaseModel`


#### class Config()
Bases: `object`


#### arbitrary_types_allowed( = True)

#### config(: foundry.models.FoundryConfig)

#### dataset(: foundry.models.FoundryDataset)

#### dc(: Optional[Dict])

#### mdf(: Optional[Dict])

### class foundry.models.FoundrySpecification(\*, name: str = '', version: str = '', description: str = '', private: bool = False, dependencies: Any = None)
Bases: `pydantic.main.BaseModel`

Pydantic base class for interacting with the Foundry data package specification
The specification provides a way to group datasets and manage versions


#### add_dependency(name, version)

#### clear_dependencies()

#### dependencies(: Any)

#### description(: str)

#### name(: str)

#### private(: bool)

#### remove_duplicate_dependencies()

#### version(: str)

### class foundry.models.FoundrySpecificationDataset(\*, name: str = None, provider: str = 'MDF', version: str = None)
Bases: `pydantic.main.BaseModel`

Pydantic base class for datasets within the Foundry data package specification


#### name(: Optional[str])

#### provider(: Optional[str])

#### version(: Optional[str])

### class foundry.models.FoundrySplit(\*, type: str = '', path: str = '', label: str = '')
Bases: `pydantic.main.BaseModel`


#### label(: Optional[str])

#### path(: Optional[str])

#### type(: str)
## foundry.xtract_method module


### foundry.xtract_method.xtract_https_download(foundryObj, verbose=False, \*\*kwargs)
## Module contents
