# elasticsearch-sync
ElasticSearch and MongoDB sync package for Meteor


## How to use
Add to meteor app -  

Add with meteor
```bash
$ meteor add toystars:elasticsearch-sync
```
Add with iron
```bash
$ iron add toystars:elasticsearch-sync
```

## Sample usage
After adding package to meteor app

```javascript

// initialize package as below

let finalCallBack = () => {
  // whatever code to run after package init
  .
  .
}

let transformFunction = (watcher, document, callBack) => {
  document.name = document.firstName + ' ' + document.lastName;
  callBack(document);
}

let sampleWatcher = {
  collectionName: 'users',
  index: 'person',
  type: 'users',
  transformFunction: transformFunction,
  fetchExistingDocuments: true,
  priority: SearchService.generics.indexOf(type) !== -1 ? 0 : 1
};

let watcherArray = [];
watcherArray.push(sampleWatcher);

let batchCount = 500;

ESMongoSync.init(null, null, finalCallBack, watcherArray, batchCount);

```

## More usage info

The elasticsearch-sync package tries as much as possible to handle most heavy lifting, but certain checks has to be put in place, and that can be seen from the init function above. The ESMongoSync.init() takes five parameters:

- **MongoDB URL** - MongoDB database to tail and pull data from.

- **ElasticSearch URL** - URL to a running ElasticSearch cluster.

- **CallBack Function** - Function to execute after initial package setup is successful (can be null).

- **Watchers** - Array of watcher objects to signify which collection to tail and receive real-time update for.

- **Batch Count** - An integer that specifies number of documents to send to ElasticSearch in batches. (can be set to very high number. defaults to 100)


Below is more info about sample watcher:

```javascript
let sampleWatcher = {
  collectionName: 'users', 
  index: 'person',
  type: 'users',
  transformFunction: transformFunction,
  fetchExistingDocuments: true,
  priority: 0
};
```

- **collectionName** - MongoDB collection to watch.

- **index** - ElasticSearch index where documents from watcher collection is saved.

- **type** - ElasticSearch type given to documents from watcher collection

- **transformFunction** - Function that gets run each time watcher document is processed. Takes 3 parameters (watcher object, document and callBack function). The callBack function is to be called with processed document as argument. (can be null)

- **fetchExistingDocuments** - Specifies if existing documents in collection are to be pulled on initialization

- **priority** - Integer (starts from 0). Useful if certain watcher depends on other watchers. Watchers with lower priorities get processed before watchers with higher priorities.


## Sample init:

Still confused? Get inspired by this [Sample SetUp](SAMPLE.js)


## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Contributions are **welcome** and will be fully **credited**.

We accept contributions via Pull Requests on [Github](https://github.com/toystars/elasticsearch-sync).


### Pull Requests

- **Document any change in behaviour** - Make sure the `README.md` and any other relevant documentation are kept up-to-date.

- **Consider our release cycle** - We try to follow [SemVer v2.0.0](http://semver.org/). Randomly breaking public APIs is not an option.

- **Create feature branches** - Don't ask us to pull from your master branch.

- **One pull request per feature** - If you want to do more than one thing, send multiple pull requests.

- **Send coherent history** - Make sure each individual commit in your pull request is meaningful. If you had to make multiple intermediate commits while developing, please [squash them](http://www.git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Changing-Multiple-Commit-Messages) before submitting.


## Issues

Check issues for current issues.

## Credits

- [Mustapha Babatunde](https://twitter.com/iAmToystars)

## License

The MIT License (MIT). Please see [LICENSE](LICENSE.md) for more information.

