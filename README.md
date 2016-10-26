# elk-stack

An [Ansible Container project](https://github.com/ansible/ansible-container) that stands up an Elastic (or ELK) Stack. Use this project 
as a starting point for your own ELK Stack project by running the following:

```
# Create an empty project directory
$ mkdir my-elk-stack 

# Set the current working directory to the new project directory
$ cd my-elk-stack

# Initialize your new project with this project
$ ansible-container init choucknecht.elk-stack
```

You now have your own *elk-stack* project that you can customize to fit your needs. If you're not sure where to start, take a look 
at the following: 

- [container.yml](./ansible/container.yml) - the orchestration document containing the Docker Compose used to start the containers
- [main.yml](./ansible/main.yml) - the playbook used to build the images. Install more logstash plugins, add custom indexes, and make any other changes
by adding additional tasks and roles to this playbook.kk 
- [Ansible Container docs](https://docs.ansible.com/ansible-container) - learn more about how to build microservice apps using Ansible Container.

## Running the application

You can run the application with sample data or without. If you wish to load some sample Apache log data, modify [main.yml](./ansible/main.yml) by setting
*create_example: true*. The modified file will look like:

```
  - role: create_example
    create_example: true
```

To run the application, build the Docker images for the app, then run containers based on those built images by executing the following commands:

# Set the working directory to your project root
$ cd my-elk-stack

# Build the elk-stack Docker images
$ ansible-container build

# Run the elk-stack application using the new images
$ ansible-container run
```

### Access the Kibana web site

Once you have the ELK stack up running, you can access the Kibana server on port 5601 of your Docker Engine host. If you're running
Docker Machine, then you should be able to do the following from a terminal session, replacing the word *default* with the name of 
your Docker Machine instance:

```
$ open http://$(docker-machine ip default):5601
```

### View the sample data

If you loaded the sample Apache data, go to Settings > Indices, and change the *Index name or pattern* value to `apache_elk_example`. When it
becomes visible, click the green *Create* button. Click on the *Discover* menu to view the data.

### Load the sample dashboard

If you loaded the sample data, go to Settings > Objects, and click Import. Select the *apache_kibana.json* file found in your the root directory of
your project. After the file loads, click on the *Dashboard* ment to see the sample dashbaord:

<img src="./dashboard.png" /> 


## Requirements

- [Ansible Container](https://github.com/ansible/ansible-container)

## Dependencies

Uses the following roles, which are automatically installed when you run `ansible-container build`:

- [chouseknecht.elasticsearch-container](https://galaxy.ansible.com/chouseknecht/elasticsearch-container)
- [chouseknecht.logstash-container](https://galaxy.ansible.com/chouseknecht/logstash-container)
- [chouseknecht.kibana-container](https://galaxy.ansible.com/chouseknecht/kibana-container)

## Author

[@chouseknecht](https://github.com/chouseknecht)
