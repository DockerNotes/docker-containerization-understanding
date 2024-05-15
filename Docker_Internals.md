Docker Internals
----------------
### Lets Start From Container
* Container can be defined as isolation with some resource limits
![Preview](./Images/di.png)
* So, host system can create multiple different containers
![Preview](./Images/di1.png)
### How are Isolations Created & Resource Limits Applied ?
* Isolations on the linux machines are created using a linux kernel feature called Namespaces. for more info [Refer Here](https://en.wikipedia.org/wiki/Linux_namespaces)
* Resource Limits are applied using kernel feature called as cgroups (Control groups). For more info [Refer Here](https://en.wikipedia.org/wiki/Cgroups)
![Preview](./Images/di2.png)
* Working on namespaces & cgroups are difficult, but here comes the docker to the rescue.
* Docker Engine makes it easy to create isolated areas & resource limits
![Preview](./Images/di3.png)
### Namespaces
* Namespaces is a linux feature.
* There is an interesting article on namespaces over [Refer Here](https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces)

__you can skip code & look at images__
* To be very specific,
    * pID namespace (Process Namespace) creates the isolated process tree inside container
    ![Preview](./Images/di4.png)

__note this is link to image from this__ [<ins>article</ins>](https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces)
* net namespace (Network Namespace) creates the isolated networking for each container with its own network interface. 
![Preview](./Images/di5)

__note this is link to image from this__ [<ins>article</ins>](https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces)
* **mount** namespace creation allows each container to have a different view of entire systems mount point, this allows containers to have their own file system view which starts from root

![Preview](./Images/di6.png)

__note this is link to image from this__ [article]
* **user** namespace allows to create whole new set of user & groups for the containers
* Fortunately even in windows world we have namespaces now. The purpose of the namespace is same but underlying implementation differs. Refer this [<ins>article</ins>](https://learn.microsoft.com/en-us/archive/msdn-magazine/2017/april/containers-bringing-docker-to-windows-developers-with-windows-server-containers)

### cgroups (control groups)
* cgroups is a linux kernel feature
* Control groups is used to impose limits. We can impose limits of disk io, RAM & cpu’s using ControlGroups
* Fortunately even in windows world we have control groups now. The purpose of the namespace is same but underlying implementation differs. Refer this [<ins>article</ins>](https://learn.microsoft.com/en-us/archive/msdn-magazine/2017/april/containers-bringing-docker-to-windows-developers-with-windows-server-containers)

### Containers also have Layers for Filesystems
_This will be discussed in another article very soon_.
#### Docker Underlying Components
The underlying components of docker as per the latest implementation is looking as shown
![Preview](./Images/di7.png)

The Specific Linux Implementation will be shown below
![Preview](./Images/di8.png)

The Specific Windows Implementation will be as shown below
![Preview](./Images/di9.png)



