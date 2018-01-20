# Ansible Container Workshop

Agenda:

 1. Running default python http server in a container.
 2. [ansible/ansible-container-demo](https://github.com/ansible/ansible-container-demo)


## "Hello World" project

[The most important link.](http://docs.ansible.com/ansible-container/)


### Install it

```
$ pip2 install --user ansible-container[docker]
```


### Ehm, what does the project look like?

We'll do

```
$ python3 -m http.server 9000
```

in a container

```
$ docker run --rm fedora:27 python3 -m http.server 9000
```


### Workspace

We'll spend the whole time inside directory `hello`. That's our project.

```
$ mkdir hello && cd hello
```


### `container.yml`

```
$ cat container.yml
settings:
  conductor:
    base: 'fedora:26'

services:
  web:
    from: 'fedora:26'
    command: ['python3', '-m', 'http.server', '--bind', '0.0.0.0', '9000']
```

Let's build it and run it:

```
$ ansible-container build
$ ansible-container run
```


### What's next?


* Expose port to host:
  ```
  ports: ["9000:9000"]
  ```

* Enable selecting the dir to serve:
  ```
  defaults:
    workdir: "/etc"
  ```
  ```
      working_dir: '{{ workdir }}'
  ```

* I also want to put my files in.
  * For that, we need add an Ansible role which will copy them.


### Orchestrated
