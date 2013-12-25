# {{.Pkg.git.name}}-ruby

{{if .Pkg.official}}Official {{end}}{{.Pkg.name}} API library client for ruby

__This library is generated by [alpaca](https://github.com/pksunkara/alpaca)__

## Installation

Make sure you have [pip](https://pypi.python.org/pypi/pip) installed

```bash
$ pip install {{.Pkg.package}}
```

## Usage

```python
import {{call .Fnc.underscore .Pkg.name}}

# Then we instantiate a client (as shown below)
```

### Build a client

##### Without any authentication

```python
client = {{call .Fnc.underscore .Pkg.name}}.Client()

# If you need to send options
client = {{call .Fnc.underscore .Pkg.name}}.Client({}, options)
```
{{if .Api.authorization.basic}}
##### Basic authentication

```python
auth = { 'username': 'pksunkara', 'password': 'password' }

client = {{call .Fnc.underscore .Pkg.name}}.Client(auth, options)
```
{{end}}{{if .Api.authorization.header}}
##### Authorization header token

```python
client = {{call .Fnc.underscore .Pkg.name}}.Client({{if .Api.authorization.oauth}}{'http_header': '1a2b3'}{{else}}'1a2b3'{{end}}, options)
```
{{end}}{{if .Api.authorization.oauth}}
##### Oauth acess token

```python
client = {{call .Fnc.underscore .Pkg.name}}.Client('1a2b3', options)
```

##### Oauth client secret

```python
auth = { 'client_id': '09a8b7', 'client_secret': '1a2b3' }

client = {{call .Fnc.underscore .Pkg.name}}.Client(auth, options)
```
{{end}}
### Response information

```python
response = client.klass('args').method('args')

response.body
# >>> 'Hello world!'

response.code
# >>> 200

response.headers
# >>> {'content-type': 'text/html'}
```
##### HTML response

```python
response.body
# >>> 'The username is pksunkara!'
```
{{if .Api.response.formats.json}}
##### JSON response

```python
response.body
# >>> {'user': 'pksunkara'}
```
{{end}}
### Request body information

##### RAW request

```python
body = 'username=pksunkara'
```

##### FORM request

```python
body = {'user': 'pksunkara'}
```
{{if .Api.request.formats.json}}
##### JSON request

```python
body = {'user': 'pksunkara'}
```
{{end}}
{{with $data := .}}{{range .Api.classes}}
### {{index $data.Doc . "title"}} api

{{index $data.Doc . "desc"}}

```python
{{call $data.Fnc.underscore .}} = client.{{call $data.Fnc.underscore .}}({{call $data.Fnc.args.python (index $data.Api.class . "args") true}})
```
{{with $class := .}}{{range $index, $element := (index $data.Api.class .)}}{{if (ne $index "args")}}
##### {{index $data.Doc $class $index "title"}} ({{call $data.Fnc.upper (or (index $element "method") "get")}} {{index $element "path"}})

{{index $data.Doc $class $index "desc"}}

```python
response = {{call $data.Fnc.underscore $class}}.{{call $data.Fnc.underscore $index}}({{call $data.Fnc.args.python (index $element "params")}}options)
```
{{end}}{{end}}{{end}}{{end}}{{end}}
## Contributors
Here is a list of [Contributors]((https://{{.Pkg.git.site}}/{{.Pkg.git.user}}/{{.Pkg.git.name}}-node/contributors)

### TODO

## License
{{.Pkg.license}}

## Bug Reports
Report [here](https://{{.Pkg.git.site}}/{{.Pkg.git.user}}/{{.Pkg.git.name}}-node/issues).

## Contact
{{.Pkg.author.name}} ({{.Pkg.author.email}})