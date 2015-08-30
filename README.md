# ca_access_control

This repository is a public repository of code used in the ConnectedAberdeen WiFi project.

Currently being developed for TillyZone project - project managed by dot.rural and SHMU in Aberdeen, Scotland.

## Architecture

HTTP request is intercepted by iptables in linux, destination IP and PORT changed to IP and TCP port 8010 of where `redirector` script runs. `redirector` will redirect the user to a new URL (where `auth_web_test` runs (TCP port 8011)) and will include connection_token GET parameter in thin new link - this parameter identifies the request. `auth_web_server` will 'authenticate' user and decide whether the user is allowed or not allowed to use internet - if the user is allowed, the `auth_web_server` will make an JSON HTTP POST API call to `auth_api` URL (TCP port 8012) which will call iptables commands to disable the very first redirect of HTTP request to `redirector` which will effectively enable internet for the user.
