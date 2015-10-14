# Purpose

Create a demonstrable application stack from `haproxy` with either `nginx` or 
`apache` as a backend.

# Usage

You will need to replace the environment variables for the `dynamic-haproxy` 
service.  

* SE_API_TOKEN:  This is your Container Application Center (CAC) API Token. 
  It is used by `confd` to connect to the CAC Service Discovery layer.
* SE_LEADER_IP: The private IP address of the mesh leader.  
* SE_SERVICE_DISCOVERY_KEY: The portion of the service discovery 
  key to check for changes. Backends to `haproxy` are written based on 
  the values of these keys. (See below for how to construct them.)

## Constructing a Service Discovery Key and Range

The construction of a Service Discovery key is done as follows:

* {{application_instance_name}} + "-" + {{service_name}} + "-" 
  + {{exposed_ port}} 

The `application_instance_name` is what you set when clicking the
"Launch" button.

The `service_name` is defined when dragging a component into the editor 
graphically as the "Name".  It is also seen as the service name in the YAML.

The `exposed_port` is the _internally_ exposed port for the backend container. 
For both nginx and apache this will be 80.   

In the case of `haproxy-nginx.yml`, that would be the line reading 
"nginx-backend-eg".

So, given that you name an application "haproxy-test" and the nginx backends
"my-backend", and that nginx is listening on port 80 inside the container you 
would have the service discovery key:

`haproxy-test-my-backend-80` 

# Contributing

If you would like to contribute to this project, please follow the standard
fork-and-pr method.  

Some things we know we would like:

* Get rid of the need to specify a key and a range
* Provide a more hardened default configuration for `haproxy`
* Make the `haproxy` configuration more flexible at run time.

# License

MIT