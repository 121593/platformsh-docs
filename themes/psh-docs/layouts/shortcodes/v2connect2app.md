{{ $serviceName := .Get "serviceName" }}
{{ $relationship := .Get "relationship" }}
{{ $var := .Get "var" }}

This configuration defines a single application `myapp`, whose source code exists in the directory `<PROJECT_ROOT>/myapp`, and has been provided access to the service (`{{ $serviceName }}`) via the relationship `{{ $relationship }}`.

From this, `myapp` can retrieve access credentials to the service through the environment variable [`{{ .Site.Params.vendor.env_prefix }}_RELATIONSHIPS`](#relationship-reference). 
That variable is a base64-encoded JSON object, but can be decoded at runtime (using the built-in tool [`jq`](https://jqlang.github.io/jq/)) to provide more accessible environment variables to use within the application itself: 

{{ .Inner }}

The above file &mdash; `.environment` in the `myapp` directory &mdash; is automatically sourced by {{ .Site.Params.vendor.name }} into the runtime environment, so that the variable `{{ $var }}` can be used within the application to connect to the service. 

Note that `{{ $var }}`, and all {{ .Site.Params.vendor.name }}-provided environment variables like `{{ .Site.Params.vendor.env_prefix }}_RELATIONSHIPS`, are environment-dependent. Unlike the build produced for a given commit, they can't be reused across environments and only allow your app to connect to a single service instance on a single environment.

A file very similar to this is generated automatically for your when using the `{{ .Site.Params.vendor.cli }} ify` command to [migrate a codebase to {{ .Site.Params.vendor.name }}](/get-started).
