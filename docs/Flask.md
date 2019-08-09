We use [Flask](http://flask.pocoo.org/) as our web framework. It handles user
authentication, dataset upload, task creation, and other aspects that require
server-side interaction. It is designed to be _independent_ from the OpenML API.
This means that you can use it to create your own personal frontend for OpenML,
using the main OpenML server to provide the data. Of course, you can also link
it to your own [local OpenML setup](Local-Installation).

### Bindings to OpenML server
You can specify which OpenML server to connect to.
This is stored in the `.env` file in the main directory. It is set to the main OpenML server by default:

``` python
    ELASTICSEARCH_SERVER=https://www.openml.org/es
    OPENML_SERVER=https://www.openml.org
```

The ElasticSearch server is used to download information about datasets, tasks, flows and runs, as well as to power the frontend search. The OpenML server is used for uploading datasets, tasks, and anything else that requires calls to the OpenML API.

### Bindings to frontend
The frontend is generated by [React](https://reactjs.org/). See below for more information. The React app is loaded as a static website. This is done in Flask setup in file `server.py`.

``` python
    app = Flask(__name__, static_url_path='', static_folder='src/client')
```

We use webpack to bundle the whole React App into one file `bundle.js`. This is done by running `npm run debug`. The settings for this are in `webpack.config.js`. For instance, it defines that `client/app/openml.jsx` is the entry file for the web app.

``` python
entry: APP_DIR + '/openml.jsx',
```

It will find the React app there and load it.