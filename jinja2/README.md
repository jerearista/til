# Jinja2 Templating

## Template Designer for Jinja2

https://td4a.now.sh/

Also available as a docker container or app when dealing with sensitive data.

## Dig into existing template structures to determine the variables, imports, and undeclared vars, etc.

* http://jinja.pocoo.org/docs/dev/api/#the-meta-api
   jinja2.meta.find_undeclared_variables(ast)
   jinja2.meta.find_referenced_templates(ast)

   ```Python
   from jinja2 import Environment, PackageLoader, meta
   env = Environment(loader=PackageLoader('gummi', 'templates'))
   template_source = env.loader.get_source(env,   'page_content.html')[0]
   parsed_content = env.parse(template_source)
   meta.find_undeclared_variables(parsed_content)
   ```

* http://github.com/aromanovich/jinja2schema
