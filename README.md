# swagger-ui

I use a lot of python flask for backend APIs. This repo can just be used as a
subrepository to have a quick and dirty way to expose a swagger ui.

## How to use

This is assuming you use python flask and do not want to render other html
pages or have the static folder used for other stuff. Because in the below
explanation the location of the relevant folders get changed in the flask
config. It is also assumed that this repo is cloned into the root folder
of your project and named "swagger-ui".

### Configure flask

Set the template and static folder like so:

```
template_dir = os.path.abspath('swagger-ui')
static_dir = os.path.abspath('swagger-ui/static')
app = Flask(__name__, template_folder=template_dir, static_folder=static_dir)
```

### Add swagger template to root folder

In the root folder of your project, add a file named "swagger_template.json".
This file contains all the information about your API. See
https://editor.swagger.io/ for more information about the format. This
implementation requires the format to be JSON, not YML! You can build your API
on the website and then convert to JSON and download the generated file.

### Add endpoint to retrieve docs

In the flask code, add an endpoint so you can access the page. In this case,
it is added to /docs:

```
@app.route('/docs')
def get_docs():
    return render_template('swaggerui.html')
```

### Add endpoint to retrieve template

Lastly, you also need an endpoint to retrieve the template:

```
@app.route('/swagger_template')
def get_swagger_template():
    with open("swagger_template.json") as f:
        return f.read()
```

